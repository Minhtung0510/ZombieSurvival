# HƯỚ DẪN LAYOUT MAP CHI TIẾT
## Dead Zone Survival — Map Layout Guide v1.0

---

# PHẦN I — TỔNG QUAN CẤU TRÚC SCENE

## 1.1 Tổng quan các Scene

| Scene | Kích thước | Ghi chú |
|---|---|---|
| **MainMenu** | — | Menu chính (không có gameplay) |
| **Hub_FireStation** | 80×80m | Safe zone — không zombie |
| **Tutorial_OldTown** | 150×150m | Tutorial — Act 1 |
| **Northside** | 200×200m | Act 1-2 |
| **Hospital_StMargaret** | 60×60m, 8 tầng | Act 2 |
| **Mall_Oakwood** | 120×120m, 3 tầng | Act 2-3 |
| **HelixTower** | 40×40m, 18 tầng | Act 3 |
| **Harbor** | 300×200m | Act 4 |
| **Eastside** | 150×150m | Act 4 — Kết thúc |
| **EvacuationPoint** | 50×50m | Wave cuối — Endgame |

## 1.2 Kết nối giữa các Scene

```
                                    [MAIN MENU]
                                          │
                                          ▼
                               [Hub_FireStation]
                                     (SAFE ZONE)
                                          │
                    ┌─────────────────────┼─────────────────────┐
                    │                     │                     │
                    ▼                     ▼                     ▼
           [Tutorial_OldTown]      [Northside]           [Eastside]
              (Act 1)                (Act 1-2)           (Act 4)
                    │                     │                     │
                    └─────────┬───────────┘                     │
                              │                                 │
                              ▼                                 │
                       [Hospital_StMargaret] ◄────────────────┘
                              │                                 │
                              │                                 │
                       ┌──────┴──────────────────────────────┐  │
                       │                                     │  │
                       ▼                                     ▼  │
                  [Mall_Oakwood]                        [HelixTower]
                  (Act 2-3)                               (Act 3)
                       │                                     │
                       └──────────────┬──────────────────────┘  │
                                      │                          │
                                      ▼                          │
                                  [Harbor]                      │
                                  (Act 4)                       │
                                      │                          │
                                      └──────────────────────────┘
                                               │
                                               ▼
                                    [EvacuationPoint]
                                        (Endgame)
```

**Quy tắc chuyển scene:**
- Người chơi đi qua **Portal Trigger** → Server load scene mới → Tất cả client load theo
- Loading screen: 2-3 giây với cinematic fade (đen → hiện scene mới)
- Tên loading screen: *"Đang rời khỏi [tên khu vực]..."*

## 1.3 Hệ thống Portal

```csharp
public class ScenePortal : MonoBehaviour
{
    public string targetScene;
    public Vector3 spawnPosition;
    public Vector3 spawnRotation;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            if (isServer)
            {
                // Chuyển scene + spawn người chơi ở vị trí mới
                NetworkManager.singleton.ServerChangeScene(targetScene);
            }
        }
    }
}
```

---

# PHẦN II — SCENE 0: HUB FIRE STATION

**Tên Scene:** Hub_FireStation
**Kích thước:** 80×80m (mặt bằng), 2 tầng + sân thượng
**Chức năng:** Safe zone — Hub chính của game

## 2.1 Layout tổng quan

```
                              [SÂN THƯỢNG - ROOFTOP]
                              ║                      ║
                              ║   [HeliSpot]        ║
                              ║   ═══════════       ║
                              ║   (Helipad)         ║
                              ╠══════════════════════╣
                              ║                      ║
         ══════════════════════╬══════════════════════╬══════════════════════
         ║  PHÒNG ĂN          ║  PHÒNG NGỦ         ║  PHÒNG LÃNH ĐẠO  ║
         ║  (Dining)          ║  (Sleeping)        ║  (Leader Room)    ║
         ║  [NPC: Survivor]   ║  [NPC: Survivor]   ║  [NPC: Elena]     ║
         ║                    ║                    ║  [Elena Quest]    ║
         ╠════════════════════╬════════════════════╬══════════════════╣
         ║  [Wardrobe]        ║  [Trạm Sửa Chữa]  ║                  ║
         ║  (Trang phục)     ║  (Workshop)        ║                  ║
         ║                    ║  [Weapon Upgrade]  ║                  ║
         ╠════════════════════╬════════════════════╬══════════════════╣
         ║                    ║                    ║                  ║
         ║         ╔══════════╩════════════════════╩══════════╗       ║
         ║         ║                                         ║       ║
         ║         ║           SÂN TRONG (Courtyard)        ║       ║
         ║         ║   [Campfire] [Storage] [Boarding]      ║       ║
         ║         ║                                         ║       ║
         ║         ╠═════════════════════════════════════════╣       ║
         ║         ║              GARAGE                     ║       ║
         ║         ║    [Fire Truck - không hoạt động]      ║       ║
         ║         ║    [Supply Crate x3]                   ║       ║
         ║         ╠═════════════════════════════════════════╣       ║
         ║         ║    [CỬA LỚN - ENTRANCE]               ║       ║
         ║         ║         ↓ [Portal → OldTown]           ║       ║
         ╚═════════╩═════════════════════════════════════════╩═══════╝
```

## 2.2 Chi tiết từng khu vực

### KHU A — SÂN TRONG (Courtyard)

```
┌─────────────────────────────────────────┐
│          SÂN TRONG                      │
│                                         │
│    [Storage]         [Campfire]         │
│    ═══════          ═══════════        │
│    (Supply x3)      (Safe ambient)       │
│                                         │
│              [MAP BOARD]                │
│           (Mission Select)               │
│                                         │
│    [Boarding]        [Notice Board]     │
│    (Barrier)         (Survivor list)   │
│                                         │
│  ←─────── ENTRANCE ─────────→          │
└─────────────────────────────────────────┘
```

- **MAP BOARD:** Interactive — người chơi mở ra xem bản đồ thành phố, chọn nhiệm vụ tiếp theo
- **Notice Board:** Gắn danh sách người mất tích (một số tên quen thuộc)
- **Storage:** 3 thùng supply (respawn mỗi ngày trong game)
- **Campfire:** Nguồn sáng ambient, có thể ngồi nghỉ (âm thanh: lửa cháy, gỗ kẽt)

### KHU B — PHÒNG ĂN (Dining Hall)

```
┌───────────────────────────────────────┐
│        PHÒNG ĂN                       │
│                                       │
│   ┌──────────┐    ┌──────────┐       │
│   │  Table 1 │    │  Table 2 │       │
│   │ [NPC]    │    │ [NPC]    │       │
│   └──────────┘    └──────────┘       │
│                                       │
│          [Kitchen Bar]                │
│          ══════════════               │
│                                       │
│   [JOURNAL ENTRY] ← bàn ở góc        │
│   (tìm được ở đây)                   │
│                                       │
│   [NPC: Tom - Survivor]               │
│   "Tôi đã thấy Shadow ở bến cảng..." │
└───────────────────────────────────────┘
```

### KHU C — PHÒNG LÃNH ĐẠO (Leader Room)

```
┌───────────────────────────────────────┐
│       PHÒNG LÃNH ĐẠO                 │
│                                       │
│   ┌──────────────────────────┐       │
│   │    [MISSION BOARD]       │       │
│   │    (Active Quests)       │       │
│   │    ☐ Main Quest          │       │
│   │    ☐ Side Quest          │       │
│   └──────────────────────────┘       │
│                                       │
│          [ELENA VASQUEZ]              │
│             (NPC)                     │
│    "Chào, Marcus. Chúng ta cần       │
│     nói về kế hoạch sơ cua."         │
│                                       │
│   [CRAFTER] ← bàn ở góc phải         │
│   [Weapon Workbench]                  │
│   [Upgrade Station]                   │
└───────────────────────────────────────┘
```

### KHU D — GARAGE

```
┌───────────────────────────────────────┐
│           GARAGE                      │
│                                       │
│   ╔═══════════════════════════════╗  │
│   ║      FIRE TRUCK               ║  │
│   ║      (không hoạt động)        ║  │
│   ║      [decorative only]        ║  │
│   ╚═══════════════════════════════╝  │
│                                       │
│   [Supply Crate 1]  [Supply Crate 2] │
│   (Loot tier: Common)   (Loot: Rare) │
│                                       │
│   [Weapon Locker - đã mở]           │
│   (Spawn: 1 weapon random)            │
│                                       │
│   ════════════════════════════════   │
│   [CỬA LỚN - ENTRANCE PORTAL]       │
│   [Portal → Tutorial_OldTown]        │
└───────────────────────────────────────┘
```

### KHU E — SÂN THƯỢNG (Rooftop)

```
┌───────────────────────────────────────────┐
│              SÂN THƯỢNG                   │
│                                           │
│      [HeliSpot]                           │
│    ════════════════════                   │
│    ║     HELIPAD        ║                  │
│    ║                   ║                  │
│    ╚═══════════════════╝                  │
│                                           │
│   [Night view - nhìn toàn cảnh TP]        │
│   (Có thể thấy 1 zombie ở xa)            │
│                                           │
│   [Supply Drop Point]                      │
│   (Respawn: 1 lần/ngày game)              │
│                                           │
│   [NPC: Watchman]                         │
│   "Có gì động ở phía Tây..."             │
└───────────────────────────────────────────┘
```

## 2.3 Spawn Points cho Portal

| Từ Hub → | Vị trí Portal | Đến → | Spawn ở đâu |
|---|---|---|---|
| Hub → OldTown | Cửa lớn | OldTown → Start House | Cửa trước căn nhà hoang |
| Hub → Northside | Cửa sườn phải | Northside → Blockade | Đầu khu dân cư |
| Hub → Eastside | Cửa sườn trái | Eastside → Alley | Đầu hẻm phía Đông |

---

# PHẦN III — SCENE 1: TUTORIAL OLD TOWN

**Tên Scene:** Tutorial_OldTown
**Kích thước:** 150×150m
**Chức năng:** Tutorial — Act 1 — Nơi Marcus tỉnh dậy
**Tone:** Ẩm ướt, hoang phế, bình minh

## 3.1 Layout tổng quan

```
                    [ĐƯỜNG CHÍNH - MAIN STREET]
                    ════════════════════════════════
                         │
    ┌────────────────────┼────────────────────┐
    │                    │                    │
    │   ┌──────────┐     │     ┌──────────┐   │
    │   │ COFFEE   │     │     │  BANK    │   │
    │   │ "Morning │     │     │ (Locked) │   │
    │   │  Star"   │     │     │  Loot:Rare│  │
    │   │[Loot:Cmn]│     │     └──────────┘   │
    │   └────┬─────┘     │                    │
    │        │           │     ┌──────────┐   │
    │        │           │     │ BOOK     │   │
    │        │           │     │ "Green-  │   │
    │        │           │     │  lake"    │   │
    │        │           │     │[AudioLog]│   │
    │        │           │     └──────────┘   │
    │        │           │                    │
    │        ▼           │         │          │
    │  ┌───────────┐     │         │          │
    │  │START HOUSE│     │         ▼          │
    │  │(Marcus)   │     │   [QUẢNG TRƯỜNG]   │
    │  │═════╤═════│     │      [Statue]      │
    │  │     │     │     │   [Shotgun loot]   │
    │  │[Z1] │[Z2] │     │      [Zombie x3]   │
    │  └─────┼─────┘     │                    │
    │        │           │         │          │
    └────────┼───────────┼─────────┼──────────┘
             │           │         │
             ▼           │         ▼
      [HẺM NHỎ]         │    [CỬA HÀNG]
       (Shortcut)        │     [GROCERY]
                         │    [Loot:Medkit]
                         │    [Zombie x2]
                         │
                         ▼
                   [ĐƯỜNG RA]
                   ↓ Portal
                   → Hub_FireStation
```

## 3.2 Chi tiết từng khu vực

### KHU A — START HOUSE (Căn nhà Marcus tỉnh dậy)

```
        MẶT BẰNG TẦNG 1 (40×30m)
        ┌─────────────────────────────────┐
        │                                 │
        │   [PHÒNG KHÁCH]    [PHÒNG NGỦ]  │
        │   (Wake up here)    [Balô]      │
        │   [Tutorial: WASD]   (Weapon)    │
        │          [P]              [B]     │
        │                                 │
        │         [HÀNH LANG]             │
        │              │                   │
        │   [KITCHEN] │                   │
        │   [Fridge]  │                   │
        │      [K]     │                   │
        │             ▼                   │
        │   ┌──────────────────────┐      │
        │   │   CỬA SỔ (Bẻ KÍNH)  │      │
        │   │   Tutorial: Jump     │      │
        │   │   [J] → Ra ngoài     │      │
        │   └──────────────────────┘      │
        └─────────────────────────────────┘
```

- **PHÒNG KHÁCH:** Điểm bắt đầu. Người chơi tỉnh dậy trên sofa.
- **PHÒNG NGỦ:** Có balô chiến thuật với M1911 + băng kit + tờ giấy
- **Tờ giấy:** *"Tầng dưới. Tìm câu trả lời. — M.C."*
- **CỬA SỔ:** Bẻ kính nhảy ra ngoài → bắt đầu tutorial bắn

### KHU B — QUẢNG TRƯỜNG (Plaza)

```
        QUẢNG TRƯỜNG (60×60m)
        ┌───────────────────────────────────┐
        │                                   │
        │          ╔═══════════╗            │
        │          ║  TƯỢNG    ║            │
        │          ║  ĐÁNH CÁ ║            │
        │          ║  (Người   ║            │
        │          ║   đánh cá)║            │
        │          ╚═══════════╝            │
        │                                   │
        │   [SHOTGUN]    [GAS STATION]     │
        │   (Under)      [Shop]            │
        │   [Hidden]     [Medkit]          │
        │                                   │
        │        [Z1]  [Z2]  [Z3]          │
        │         ☠    ☠    ☠             │
        │        (Walker)                  │
        │                                   │
        │   [DUMPSTER]    [BENCH]          │
        │   [Ammo:10]     [Graffiti]       │
        │                                   │
        │   [FLOWER STAND]  [TRASH]        │
        │   (Deco)          (Ammo x5)      │
        │                                   │
        │  ←── ĐƯỜNG CHÍNH ──→             │
        │       [Zombie x2 patrol]          │
        └───────────────────────────────────┘
```

- **TƯỢNG ĐÁNH CÁ:** Trung tâm quảng trường, có thể trèo lên làm cover
- **SHOTGUN:** Che giấu dưới tượng, tutorial bắn sẽ dẫn đến đây
- **ZOMBIE:** 3 Walker patrol quảng trường (Tutorial combat)
- **GRAFFITI:** *"HELIX LIAR"* trên băng đá

### KHU C — COFFEE SHOP "Morning Star"

```
        MẶT BẰNG (20×20m)
        ┌─────────────────────┐
        │    [COUNTER]        │
        │    ═══════════      │
        │    [Barista body]   │
        │                     │
        │  ┌───────┐ ┌─────┐ │
        │  │ TABLE │ │TABLE│ │
        │  │       │ │     │ │
        │  │ [P1] │ │[P2] │ │
        │  └───────┘ └─────┘ │
        │                     │
        │    [KITCHEN]        │
        │    [Back door]      │
        │    (→ Hẻm nhỏ)     │
        │         ↓           │
        └─────────────────────┘
```

- **Loot:** Counter có băng kit (Uncommon tier)
- **Back door:** Lối ra hẻm nhỏ (shortcut về Start House)
- **Body:** Xác barista trên counter (have been turned)

### KHU D — MAIN STREET (Đường chính)

```
        ĐOẠN ĐƯỜNG CHÍNH (150×30m)
        ═══════════════════════════════════════
             [Street light]   [Street light]
                  │               │
        ──────────┼───────────────┼──────────────
        │         │               │              │
        │ [CAR1]  │   [ZOMBIE]    │   [CAR2]    │
        │ (cover) │   x2 patrol   │   (cover)   │
        │         │               │              │
        │         ▼               │              │
        │    [CROSSWALK]          │              │
        │                         │              │
        │  [Billboard]            │              │
        │  "GREENLAKE             │              │
        │   - Where Life          │              │
        │    Begins-"             │              │
        │  (falling apart)        │              │
        │                         │              │
        ──────────┬───────────────┼──────────────
                  │               │
             [ZOMBIE]        [ZOMBIE]
             (Walker)        (Runner)
             patrol          (sneaky)
```

### KHU E — Đường ra (Exit)

```
        ĐƯỜNG RA
        ┌─────────────────────────────────────┐
        │                                     │
        │    [BARRIER]    [MILITARY TRUCK]    │
        │    (cover)      (directional hint)  │
        │                                     │
        │         [ZOMBIE x2]                 │
        │          ☠  ☠                      │
        │                                     │
        │   ╔═══════════════════════════════╗  │
        │   ║   GATE / CỬA HUB             ║  │
        │   ║   [Portal → Hub_FireStation]  ║  │
        │   ║   "Trạm cứu hỏa..."         ║  │
        │   ╚═══════════════════════════════╝  │
        │                                     │
        │   [Sign] "→ FIRE STATION #7: 200m" │
        │                                     │
        └─────────────────────────────────────┘
```

## 3.3 Bảng Spawn Points

| ID | Vị trí | Loại | Số lượng | Trigger |
|---|---|---|---|---|
| Z_A1 | Quảng trường | Walker | 3 | Không — patrol sẵn |
| Z_A2 | Đường chính | Walker | 2 | Khi người chơi bước ra Start House |
| Z_A3 | Đường chính | Runner | 1 | Khi nhặt shotgun |
| Z_A4 | Grocery | Walker | 2 | Khi mở cửa grocery |
| Z_A5 | Cổng ra | Walker | 2 | Khi đến gần cổng |
| Z_B1 | Quảng trường | Walker | 3 | Wave tutorial |

## 3.4 Loot Spawners

| ID | Vị trí | Tier | Item |
|---|---|---|---|
| L_A1 | Phòng ngủ (Start House) | Common | M1911, Ammo x20 |
| L_A2 | Phòng khách (Start House) | Common | Băng kit nhỏ |
| L_A3 | Quảng trường (dưới tượng) | Rare | Remington 870 (Shotgun) |
| L_A4 | Coffee shop | Uncommon | Băng kit lớn |
| L_A5 | Dumpster | Common | Ammo x10 |
| L_A6 | Grocery | Uncommon | Medkit |

---

# PHẦN IV — SCENE 2: NORTHSIDE

**Tên Scene:** Northside
**Kích thước:** 200×200m
**Chức năng:** Act 1-2 — Khu dân cư trung lưu
**Tone:** Mưa, lạnh, nhà cửa đổ nát

## 4.1 Layout tổng quan

```
                         [ĐẠI LỘ]
                    ═══════════════════
                         │
    ┌──────────────────┼──────────────────┐
    │                  │                  │
    │  ┌──────────┐    │    ┌──────────┐  │
    │  │CHURCH   │    │    │SCHOOL    │  │
    │  │St.Joseph│    │    │Greenlake │  │
    │  │─────────│    │    │──────────│  │
    │  │[Priest] │    │    │[Classroom]│  │
    │  │[AudioL] │    │    │[AudioLog]│  │
    │  │[Z:Brute]│    │    │[Kid body] │  │
    │  │(spawn)  │    │    │[Z:x3]    │  │
    │  └──────────┘    │    └──────────┘  │
    │                  │                  │
    │     ┌────────────┼────────────┐     │
    │     │            │            │     │
    │     │   KHU DÂN  │  CƯ  TRUNG │     │
    │     │   ┌───┐    │  LUẬU     │     │
    │     │   │H1 │    │            │     │
    │     │   │H2 │    │  ┌───┐    │     │
    │     │   │H3 │    │  │H4 │    │     │
    │     │   │H4 │    │  │H5 │    │     │
    │     │   └───┘    │  │H6 │    │     │
    │     │            │  └───┘    │     │
    │     │ [Pool]    │           │     │
    │     │ (zombie)  │           │     │
    │     └────────────┴───────────┘     │
    │                  │                  │
    │  ┌──────────┐    │    ┌──────────┐  │
    │  │QUICKSTOP │    │    │PHARMA    │  │
    │  │  SHOP    │    │    │  (Locked)│  │
    │  │[Loot:Cmn]│    │    │[Loot:Rare]│ │
    │  │[Z:x2]   │    │    │[Key req] │  │
    │  └──────────┘    │    └──────────┘  │
    │                  │                  │
    └──────────────────┼──────────────────┘
                       │
                  [ĐƯỜNG RA]
                  ↓ Portal → Hospital
```

## 4.2 Chi tiết từng khu vực

### KHU A — CHÙA ST. JOSEPH (Church)

```
        MẶT BẰNG CHÙA (40×30m)
        ┌─────────────────────────────────┐
        │           THÁP CHUÔNG           │
        │         (Bell Tower)            │
        │        [Loot: Keycard]         │
        │        [Zombie: Brute x1]       │
        │                                 │
        ├─────────────────────────────────┤
        │                                 │
        │         [GIÁO ĐƯỜNG]           │
        │         (Giáo đường)           │
        │    ════════════════════         │
        │                                 │
        │   [PRIEST BODY]  [ZOMBIE x2]  │
        │   (đang cầu nguyện)   (dù mãi)│
        │        ☠               ☠        │
        │                                 │
        │   [BĂNG GHẾ]   [NẾN]          │
        │                                 │
        │         [CỬA TRƯỚC]            │
        │         (← Đường chính)        │
        └─────────────────────────────────┘
```

- **BRUTE:** Spawn trên tháp chuông — surprise khi leo lên
- **PRIESTS BODY:** Đang quỳ cầu nguyện, có journal entry
- **LOOT:** Keycard Level 2 trên tháp (mở Pharma)

### KHU B — TRƯỜNG TIỂU HỌC (School)

```
        MẶT BẰNG TRƯỜNG (50×40m)
        ┌─────────────────────────────────────┐
        │           SÂN TRƯỜNG                │
        │     [Swing - đung đưa một mình]     │
        │                                     │
        ├──────────┬──────────┬───────────────┤
        │ CLASS 1  │ CLASS 2  │  LIBRARY     │
        │ [Chair]  │ [Chair]  │ [Book]       │
        │ [Z:x1]  │ [Z:x1]  │ [AudioLog]   │
        │         │         │  (Teacher)   │
        ├──────────┴──────────┴───────────────┤
        │                                     │
        │           HÀNH LANG                │
        │     [KID'S BODY x2]               │
        │     (under table)                  │
        │            [Z:x2 Crawler]          │
        │            (ẩn nấp)               │
        │                                     │
        ├─────────────────────────────────────┤
        │         PHÒNG GIÁO VỤ              │
        │    [PRINCIPAL BODY]                │
        │    [Loot: Map]                     │
        │    (trong tủ, khóa)               │
        │                                     │
        └─────────────────────────────────────┘
```

- **CRAWLER:** Ẩn nấp trong hành lang, khó phát hiện
- **AUDIO LOG:** Giọng cô giáo: *"Các con hãy đi đi, cô sẽ ở lại đây..."*
- **MAP:** Bản đồ thành phố trong phòng giáo vụ (reveal các khu vực)

### KHU C — KHU DÂN CƯ (Residential)

```
        MỘT BLOCK DÂN CƯ (80×80m)
        ┌───────────────────────────────────────┐
        │                                       │
        │   ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐│
        │   │H1   │  │H2   │  │H3   │  │H4   ││
        │   │     │  │     │  │     │  │     ││
        │   │[Z:x1]│  │[Z:x1]│  │[L]  │  │[Z:x2]││
        │   └─────┘  └─────┘  └─────┘  └─────┘│
        │                                       │
        │   ══════════ ĐƯỜNG NHỎ ══════════   │
        │                                       │
        │   ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐│
        │   │H5   │  │H6   │  │H7   │  │H8   ││
        │   │     │  │Pool │  │     │  │     ││
        │   │[Z:x1]│  │     │  │[L]  │  │[Z:x2]││
        │   └─────┘  │[Z:x3]│  └─────┘  └─────┘│
        │            │Walker│                     │
        │            │(hồ)  │                     │
        │            └──────┘                     │
        └───────────────────────────────────────┘

        L = Loot spawner | Z = Zombie spawn
```

- **H1-H8:** Mỗi nhà có thể vào, bên trong có furniture + zombie
- **POOL:** Hồ bơi trong vắt, có zombie bơi (Walker underwater variant)
- **LOOT:** 50% nhà có loot (Common tier)

### KHU D — QUICKSTOP SHOP

```
        MẶT BẰNG CỬA HÀNG (15×15m)
        ┌─────────────────────────────────┐
        │                                 │
        │    ┌───────────────────────┐    │
        │    │      QUẦY HÀNG        │    │
        │    │   [Register - broke]  │    │
        │    │   [Snacks] [Drinks]  │    │
        │    │   [Cigarette]        │    │
        │    └───────────────────────┘    │
        │                                 │
        │   [SHELF]  [SHELF]  [SHELF]   │
        │   [Food]   [Food]   [Ammo x15]│
        │                                 │
        │      [ZOMBIE x2]               │
        │       ☠  ☠                     │
        │    (store clerk)               │
        │                                 │
        │         [EXIT]                 │
        └─────────────────────────────────┘
```

### KHU E — ĐẠI LỘ (Main Road)

```
        ĐOẠN ĐẠI LỘ (200×30m)
        ═══════════════════════════════════════════════

             [Street light]    [Street light]    [Street light]
                  │                  │                  │
        ──────────┼──────────────────┼──────────────────┼──────
        │         │                  │                  │       │
        │ [MILITARY│                │    [ABANDONED    │       │
        │  JEEP]  │                │     BUS]         │       │
        │(cover)  │                │    (cover)       │       │
        │         │                │                  │       │
        │  [Z:x2] │                │   [Z:x3 Runner]  │       │
        │ Walker  │                │   (on bus roof)   │       │
        │         │                │                  │       │
        │         ▼                │                  ▼       │
        │   [CROSSWALK]            │          [CROSSWALK]    │
        │                         │                         │
        │  [ELENA]                │                         │
        │  (NPC meeting)          │                         │
        │  "Marcus, tôi là        │                         │
        │   Elena. Đi theo tôi."  │                         │
        │                         │                         │
        │                         │                  [GATE] │
        │                         │                 [→Hosp]│
        └─────────────────────────┴─────────────────────────┘
```

- **ELENA:** NPC encounter — Elena xuất hiện, bắt đầu Act 1 storyline
- **GATE:** Portal → Hospital_StMargaret (sau khi hoàn thành M4)

## 4.3 Zombie Distribution

| Khu vực | Loại | Số lượng | Trigger |
|---|---|---|---|
| Church (Tháp) | Brute | 1 | Khi leo lên tháp |
| Church (Giáo đường) | Walker | 2 | Khi vào giáo đường |
| School (Lớp) | Walker | 2 | Khi mở cửa lớp |
| School (Hành lang) | Crawler | 2 | Khi đi qua hành lang |
| Residential (nhà) | Walker | 8 | Khi vào nhà |
| Residential (hồ) | Walker | 3 | Khi đến gần hồ |
| QuickStop | Walker | 2 | Khi vào cửa hàng |
| Đại lộ | Runner | 3 | Khi đến khu vực bus |
| Đại lộ | Walker | 2 | Khi gặp Elena |

---

# PHẦN V — SCENE 3: HOSPITAL ST. MARGARET

**Tên Scene:** Hospital_StMargaret
**Kích thước:** 60×60m mặt bằng + 8 tầng
**Chức năng:** Act 2 — Trụ sở SOS, kho thuốc
**Tone:** Tối, y tế, máu, mùi chlorine

## 5.1 Layout tầng 1 (Tầng trệt)

```
        TẦNG 1 — RECEPTION (60×60m)
        ═══════════════════════════════════════

        [PHÒNG CHỜ]          [THANG MÁY]
        ┌──────────┐          ╔══════════╗
        │ [Chair]  │          ║  ↑↓ 1-8  ║
        │ [Body]   │          ║ (không    ║
        │ [Blood]  │          ║  hoạt    ║
        │          │          ║  động)   ║
        └─────┬────┘          ╚════╤═════╝
              │                    │
        ┌─────┴────────────────────┴────┐
        │                               │
        │         LỄ TÂN                │
        │      [RECEPTION]              │
        │   ════════════════════        │
        │   [Receptionist body]        │
        │   (bị trói vào ghế)          │
        │   [Zombie: x1]               │
        │                               │
        ├────────────┬──────────────────┤
        │            │                  │
        │ [CORRIDOR│ [KOREA CAP CUỨ]  │
        │  →Ward]   │  ═══════════     │
        │           │  [Khoa cấp cứu]  │
        │           │  [Zombie x3]      │
        │           │  (Crawler x1)     │
        │           │                  │
        ├───────────┴──────────────────┤
        │                               │
        │        HÀNH LANG CHÍNH        │
        │                               │
        │   [Phòng mổ]  [Tủ thuốc]     │
        │   [Surgery]   [Pharma Loot]   │
        │   [Z:x2]     [Rare tier]     │
        │                               │
        ├───────────────────────────────┤
        │                               │
        │        CỬA SA THẢI           │
        │        [→ Basement]           │
        │        [KEY: Level 3]        │
        │                               │
        ├───────────────────────────────┤
        │                               │
        │        CỬA CHÍNH             │
        │        [← Đường ra]           │
        │        (Portal Hub)           │
        └───────────────────────────────┘
```

## 5.2 Layout tầng 2-7 (Patient Floors)

```
        TẦNG ĐIỂN HÌNH — PATIENT FLOOR (MỖI TẦNG GIỐNG NHAU)
        ═══════════════════════════════════════════════

        [PHÒNG BỆNH 1]    [PHÒNG BỆNH 2]    [PHÒNG BỆNH 3]
        ┌──────────┐      ┌──────────┐      ┌──────────┐
        │ [Bed x2] │      │ [Bed x2] │      │ [Bed x2] │
        │ [Body]   │      │ [Z:x1]   │      │ [Loot]   │
        │ [Z:x1]  │      │ (Wake up)│      │          │
        └────┬─────┘      └────┬─────┘      └────┬─────┘
             │                 │                 │
        ┌────┴─────────────────┴─────────────────┴────┐
        │                                              │
        │              HÀNH LANG                      │
        │         [NURSE STATION]                     │
        │         [Medkit: Uncommon]                  │
        │                                              │
        ├─────────────────────────────────────────────┤
        │                                              │
        │  [PHÒNG BỆNH 4]   [PHÒNG BỆNH 5]   [KHO] │
        │  ┌──────────┐    ┌──────────┐    ┌──────┐ │
        │  │ [Bed x2] │    │ [Bed x2] │    │      │ │
        │  │ [Z:x1]  │    │ [Body]   │    │[Loot]│ │
        │  └──────────┘    └──────────┘    └──────┘ │
        │                                              │
        └──────────────────────────────────────────────┘

        Mỗi tầng: 5 phòng bệnh, 1 nurse station, 1 kho
```

## 5.3 Layout Tầng 8 (Rooftop)

```
        TẦNG 8 — ROOFTOP
        ═══════════════════════

        ┌───────────────────────────────┐
        │                               │
        │      HELIPAD (ngày xưa)      │
        │      ══════════════════      │
        │      (Helicopter đã đi)      │
        │                               │
        │   [Supply Drop] ← respawn    │
        │   [Loot: Rare]              │
        │                               │
        │   [WATER TOWER]             │
        │   (Cover tốt + sniper)      │
        │                               │
        │      [JAMES PARK]            │
        │      (NPC - SOS leader)      │
        │      "Marcus, cảm ơn anh     │
        │       đã đến. Có chuyện     │
        │       ở tầng hầm..."         │
        │                               │
        │      [ELEVATOR]              │
        │      (Xuống tầng hầm)        │
        │      [KEY: Level 4 req]       │
        │                               │
        └───────────────────────────────┘
```

## 5.4 Layout Tầng Hầm (Basement)

```
        TẦNG HẦM — HELIX LAB (60×60m)
        ═══════════════════════════════════

        ┌─────────────────────────────────────┐
        │                                     │
        │   ╔═══════════════════════════════╗ │
        │   ║      PHÒNG THÍ NGHIỆM        ║ │
        │   ║   ════════════════════════   ║ │
        │   ║                               ║ │
        │   ║   [Lab Table]  [Microscope]  ║ │
        │   ║   [Specimen]   [Computer]    ║ │
        │   ║                               ║ │
        │   ║   [HELENA CROSS - Video]     ║ │
        │   ║   (Bản ghi ngày 0)          ║ │
        │   ║   [Evidence - Mission 10]   ║ │
        │   ║                               ║ │
        │   ║   [ZOMBIE x3]               ║ │
        │   ║   (Researcher zombie)       ║ │
        │   ║   (Security zombie x1)       ║ │
        │   ║                               ║ │
        │   ╚═══════════════════════════════╝ │
        │                                     │
        │   [CAMERA FEED ROOM]                │
        │   [Monitors x9]                     │
        │   (Camera khắp thành phố)           │
        │   [Helena's Office]                 │
        │   [Personal item: Sarah's photo]    │
        │   (Gợi ý: Marcus đã từng ở đây)    │
        │                                     │
        └─────────────────────────────────────┘
```

- **HELENA CROSS VIDEO:** Video ghi lại sự cố ngày 0 — bằng chứng về sai phạm Helix
- **CAMERA FEED:** Thấy các khu vực khác trên camera (xem trước map sắp đến)
- **SARAH'S PHOTO:** Trong phòng Helena — gợi ý về mối quan hệ Marcus-Helix-Sarah

## 5.5 Zombie Distribution

| Tầng | Loại | Số lượng | Đặc điểm |
|---|---|---|---|
| Tầng 1 | Walker | 3 | Reception + corridor |
| Tầng 1 | Crawler | 1 | Khoa cấp cứu (ẩn nấp) |
| Tầng 1 | Walker | 2 | Phòng mổ |
| Tầng 2-7 | Walker | 3/tầng | Phòng bệnh |
| Tầng 2-7 | Crawler | 1/tầng | Hành lang (ẩn nấp) |
| Tầng 8 | Security | 2 | Rooftop (bảo vệ James) |
| Tầng hầm | Researcher | 3 | Phòng thí nghiệm |
| Tầng hầm | Security | 1 | Camera room |

---

# PHẦN VI — SCENE 4: MALL OAKWOOD

**Tên Scene:** Mall_Oakwood
**Kích thước:** 120×120m, 3 tầng + tầng hầm
**Chức năng:** Act 2-3 — Kho vũ khí, loot tốt nhất
**Tone:** Khổng lồ, hoang tàn, nhiều Horde

## 6.1 Layout tầng 1 (Ground Floor)

```
        TẦNG 1 — GROUND FLOOR (120×120m)
        ═══════════════════════════════════════════════

        ╔════════════════════════════════════════════════╗
        ║              ATRIUM CHÍNH                      ║
        ║        (Trung tâm — sảnh lớn)                 ║
        ║    ════════════════════════════════           ║
        ║                                                ║
        ║         [FOUNTAIN]                             ║
        ║         (khô cạn, có xác)                     ║
        ║                                                ║
        ║    [ZOMBIE HORDE x5 - patrol]                 ║
        ║         ☠ ☠ ☠ ☠ ☠                             ║
        ║                                                ║
        ╚════════╤════════════════════════════════════════╛
                 │
    ┌────────────┼────────────────────────────────────┐
    │            │                                    │
    │ [FOOD      │  [RETAIL 1]  [RETAIL 2]  [RETAIL 3]│
    │  COURT]    │  [Clothing] [Shoes]   [Electronics]│
    │            │                                    │
    │  [Z:x3]   │  [L:Cmn]    [L:Cmn]    [L:Uncm]    │
    │  (Runner) │                                    │
    │            │────────────────────────────────────│
    │            │                                    │
    │            │  [MAIN CORRIDOR — ĐƯỜNG CHÍNH]     │
    │            │  ════════════════════════════════  │
    │            │                                    │
    │            │      [ZOMBIE x4]                   │
    │            │       ☠  ☠  ☠  ☠                  │
    │            │                                    │
    │            │────────────────────────────────────│
    │            │                                    │
    │            │ [BLACK RIVER     [PHONE          │
    │            │   ARMS]           STORE]          │
    │            │ [GUN SHOP]       [L:Cmn]          │
    │            │ ════════════                     │
    │            │ [LOCKED - Key]  ← Key ở food court│
    │            │ [L:Legendary]                     │
    │            │ (Assault Rifle + Ammo)            │
    │            │                                    │
    ├────────────┴────────────────────────────────────┤
    │                                                    │
    │        [ESCALATOR ↑]     [ESCALATOR ↑]           │
    │          → Tầng 2          → Tầng 2              │
    │                                                    │
    │        [STAIRS ↓]          [STAIRS ↓]             │
    │          → Tầng Hầm        → Tầng Hầm            │
    │                                                    │
    ├────────────────────────────────────────────────────┤
    │                                                    │
    │         [EMERGENCY EXIT — ĐƯỜNG RA]               │
    │         [→ Northside Portal]                      │
    │         [ZOMBIE x6 - Horde]                      │
    │         (Trigger khi đến gần)                    │
    │                                                    │
    └────────────────────────────────────────────────────┘
```

## 6.2 Layout tầng 2 (Upper Floor)

```
        TẦNG 2 — UPPER FLOOR (120×120m)
        ═══════════════════════════════════════════════

        ┌──────────────────────────────────────────────────┐
        │              ATRIUM VIEW (LOOKING DOWN)          │
        │                                                    │
        │   [ESCALATOR ↓]              [ESCALATOR ↓]        │
        └──────────────────────────────────────────────────┘

        ┌──────────────────────────────────────────────────┐
        │                                                    │
        │  [MOVIE THEATER]      [GAME STORE]    [BOOKS]   │
        │  ══════════════       ═══════════    ═════════  │
        │  [Screen - zombie]   [Z:x2]         [L:Cmn]    │
        │  [Audio: movie]     (Runner)                   │
        │  [L:Uncommon]                                         │
        │                                                    │
        ├──────────────────────────────────────────────────┤
        │                                                    │
        │  [KIDS ZONE]          [ARCADE]         [FOOD 2] │
        │  ═══════════          ═══════════     ═══════  │
        │  [PLAYGROUND]        [Machines]       [Z:x1]   │
        │  [MOTHER + CHILD]    (dead)                      │
        │  [Z:x1 Walker]                                       │
        │                                                    │
        ├──────────────────────────────────────────────────┤
        │                                                    │
        │            [UPPER CORRIDOR]                       │
        │            ═══════════════════                   │
        │                                                    │
        │    [ZOMBIE x3]        [ZOMBIE x2]                │
        │     ☠ ☠ ☠              ☠ ☠                     │
        │                                                    │
        │  [JEWELRY]        [SPA]         [SALON]         │
        │  [L:Rare]        [L:Cmn]       [Z:x1]           │
        │  (hidden)                                                  │
        │                                                    │
        ├──────────────────────────────────────────────────┤
        │                                                    │
        │   [ESCALATOR ↓]              [ESCALATOR ↓]        │
        │     → Tầng 1                  → Tầng 1           │
        │                                                    │
        │   [STAIRS ↑]                                       │
        │     → Tầng 3 (Rooftop)                            │
        │                                                    │
        └──────────────────────────────────────────────────┘
```

## 6.3 Layout tầng 3 (Rooftop)

```
        TẦNG 3 — ROOFTOP / HELIPAD (120×120m)
        ═══════════════════════════════════════════════

        ┌──────────────────────────────────────────────────┐
        │                                                  │
        │           [HELIPAD — BỎ HOANG]                  │
        │           ══════════════════════                 │
        │           (Blackout đã cướp trực thăng)         │
        │                                                  │
        │   [SUPPLY DROP]                                 │
        │   [L:Epic - random weapon]                      │
        │                                                  │
        │   [WATER TOWER x2]                             │
        │   (Cover + có thể leo lên)                     │
        │                                                  │
        │   [ZOMBIE x6]                                  │
        │   ☠ ☠ ☠ ☠ ☠ ☠                                  │
        │   (Spawn khi lên đến đây)                      │
        │   (Walker x4 + Runner x2)                       │
        │                                                  │
        │   [ANTENNA TOWER]                              │
        │   (Bẫy - có thể làm rơi)                       │
        │                                                  │
        │   [EXIT: STAIRS ↓]                             │
        │     → Tầng 2                                    │
        │                                                  │
        └──────────────────────────────────────────────────┘
```

## 6.4 Layout tầng hầm (Basement / Parking)

```
        TẦNG HẦM — PARKING (120×120m)
        ═══════════════════════════════════════════════

        ┌──────────────────────────────────────────────────┐
        │                                                   │
        │   [PARKING ROW A]     [PARKING ROW B]           │
        │   ══════════════      ══════════════            │
        │   [Car x10]          [Car x10]                 │
        │   (some zombies     (some loot)                 │
        │    inside)                                     │
        │                                                   │
        │   [ZOMBIE x4]         [ZOMBIE x4]              │
        │    ☠ ☠ ☠ ☠             ☠ ☠ ☠ ☠                 │
        │                                                   │
        ├──────────────────────────────────────────────────┤
        │                                                   │
        │              MAIN DRIVE AISLE                     │
        │          ════════════════════════                │
        │                                                   │
        │      [ZOMBIE x6 - HORDE]                        │
        │      ☠ ☠ ☠ ☠ ☠ ☠                                │
        │      (Spawn khi đi vào aisle)                    │
        │                                                   │
        ├──────────────────────────────────────────────────┤
        │                                                   │
        │   [STAIRS ↑]              [STAIRS ↑]            │
        │     → Tầng 1                → Tầng 1             │
        │                                                   │
        │   [LOADING DOCK]                                │
        │   [L:Rare - supply crate]                       │
        │   [Z:x2 Crawler]                                │
        │                                                   │
        │   [EXIT — ĐƯỜNG RA]                            │
        │   [→ Harbor Portal]                             │
        │                                                   │
        └──────────────────────────────────────────────────┘
```

## 6.5 Zombie Distribution

| Tầng | Loại | Số lượng | Trigger |
|---|---|---|---|
| Tầng 1 | Walker | 5 | Atrium (patrol) |
| Tầng 1 | Walker | 3 | Food court |
| Tầng 1 | Walker | 4 | Main corridor |
| Tầng 1 | Runner | 2 | Food court |
| Tầng 1 | Walker | 6 | Emergency exit horde |
| Tầng 2 | Walker | 2 | Movie theater |
| Tầng 2 | Runner | 2 | Game store |
| Tầng 2 | Walker | 3 | Upper corridor |
| Tầng 2 | Walker | 1 | Salon |
| Tầng 3 | Walker | 4 | Rooftop |
| Tầng 3 | Runner | 2 | Rooftop |
| Tầng Hầm | Walker | 8 | Parking |
| Tầng Hầm | Crawler | 2 | Loading dock |
| Tầng Hầm | Walker | 6 | Main aisle horde |

---

# PHẦN VII — SCENE 5: HELIX TOWER

**Tên Scene:** HelixTower
**Kích thước:** 40×40m mặt bằng + 18 tầng + 4 tầng hầm
**Chức năng:** Act 3 — Đột nhập Helix, đối đầu Bulwark
**Tone:** High-tech, sạch sẽ nhưng có vết máu, security zombie

## 7.1 Layout tầng 1 (Lobby)

```
        TẦNG 1 — LOBBY (40×40m)
        ═════════════════════════════

        ┌─────────────────────────────────┐
        │                                 │
        │   ╔═══════════════════════════╗ │
        │   ║      RECEPTION DESK       ║ │
        │   ║  [Helix Logo]            ║ │
        │   ║  [Body: receptionist]    ║ │
        │   ║  [Keycard: Level 2]      ║ │
        │   ║  [Zombie: Security x1]   ║ │
        │   ╚═══════════════════════════╝ │
        │                                 │
        │         [ELEVATOR LOBBY]      │
        │         ════════════════       │
        │         [→ All floors]         │
        │         [Level 1 access only]  │
        │                                 │
        │   [SECURITY DESK]             │
        │   [Camera monitors]           │
        │   [Zombie: Security x2]       │
        │                                 │
        ├─────────────────────────────────┤
        │                                 │
        │    [GARAGE ENTRANCE]            │
        │    ← Từ bên ngoài              │
        │    [→ Tầng Hầm 1]              │
        │                                 │
        ├─────────────────────────────────┤
        │                                 │
        │    [LOBBY EXIT]                │
        │    (→ Mall Portal)             │
        │                                 │
        └─────────────────────────────────┘
```

## 7.2 Layout tầng 2-14 (Office Floors)

```
        TẦNG ĐIỂN HÌNH — OFFICE FLOOR (40×40m)
        ═══════════════════════════════════════

        ┌───────────────────────────────────────┐
        │                                       │
        │   [CUBICLE AREA]     [MEETING ROOM]   │
        │   ═════════════     ═════════════     │
        │   [Desk x6]        │[Table x8]       │
        │   [Z:x1 Walker]    │[Z:x1 Walker]   │
        │   [L:Cmn x2]       │[L:Uncm x1]     │
        │                    │                │
        ├───────────────────┴──────────────────┤
        │                                       │
        │            HÀNH LANG                 │
        │            ═══════════               │
        │                                       │
        │   [BOSS OFFICE]      [KITCHENETTE]   │
        │   [Locked - L2]      [Z:x1 Walker]   │
        │   [L:Rare]           [L:Cmn]         │
        │                                       │
        ├───────────────────────────────────────┤
        │                                       │
        │           [ELEVATOR]                  │
        │           ═══════════                 │
        │           [→ All floors]              │
        │           [Requires level]            │
        │                                       │
        └───────────────────────────────────────┘
```

## 7.3 Layout tầng 15 (Marcus's Office)

```
        TẦNG 15 — EXECUTIVE FLOOR (40×40m)
        ═══════════════════════════════════════

        ┌───────────────────────────────────────┐
        │                                       │
        │   [CONFERENCE ROOM]                   │
        │   ════════════════════════           │
        │   [Meeting table - đầy giấy tài liệu]│
        │   [Board: "PROMETHEUS-7 - DAY 0"]    │
        │   [L:Epic - Document]                │
        │                                       │
        ├───────────────────────────────────────┤
        │                                       │
        │   [MARCUS'S OFFICE]                  │
        │   ════════════════════               │
        │   "Marcus Cole - Security"           │
        │   ════════════════════════           │
        │                                       │
        │   [Desk]                              │
        │   [Photo: Sarah + Lily]              │
        │   [Note: "I'm sorry"]                │
        │   [L:Rare - USB (evidence)]          │
        │                                       │
        │   [Window view]                       │
        │   (Nhìn xuống thành phố chết)        │
        │                                       │
        ├───────────────────────────────────────┤
        │                                       │
        │   [HALLWAY TO STAIRWELL]             │
        │   [→ Stairwell access]               │
        │   [Zombie: Security x2]               │
        │                                       │
        └───────────────────────────────────────┘
```

- **SARAH'S PHOTO:** Trên bàn — gợi ý về mối quan hệ Marcus-Sarah và công việc bảo vệ Helix
- **"I'M SORRY" NOTE:** Tờ giấy viết tay — Marcus không nhớ viết

## 7.4 Layout tầng 18 (Rooftop)

```
        TẦNG 18 — ROOFTOP (40×40m)
        ═════════════════════════════

        ┌───────────────────────────────────────┐
        │                                       │
        │          [HELIPAD]                    │
        │          ════════════════             │
        │          (Blackout đã cướp)           │
        │                                       │
        │   [UTILITY BUILDING]                 │
        │   [Generator - silent]               │
        │   [Zombie: Security x1]              │
        │                                       │
        ├───────────────────────────────────────┤
        │                                       │
        │          [STAIRWELL EXIT]             │
        │          [→ Tầng Hầm 4]              │
        │          [DOOR - Level 4 req]         │
        │                                       │
        │   [Sign]                              │
        │   "↓ SUBLEVEL 4 — R&D LAB"           │
        │                                       │
        └───────────────────────────────────────┘
```

## 7.5 Layout tầng hầm 4 (R&D Lab — BOSS ROOM)

```
        TẦNG HẦM 4 — R&D LAB (40×40m)
        ═══════════════════════════════════════

        ┌───────────────────────────────────────┐
        │                                       │
        │   ╔═════════════════════════════════╗ │
        │   ║                                 ║ │
        │   ║         BOSS ARENA             ║ │
        │   ║    ════════════════════════    ║ │
        │   ║                                 ║ │
        │   ║       [BULLWORK]                ║ │
        │   ║        (Brute Boss)             ║ │
        │   ║       HP: 500 / 200 Shield     ║ │
        │   ║                                 ║ │
        │   ║    [LAB BENCH]  [LAB BENCH]    ║ │
        │   ║    (Cover)       (Cover)       ║ │
        │   ║                                 ║ │
        │   ║    [COLUMN]    [COLUMN]       ║ │
        │   ║    (Cover)       (Cover)       ║ │
        │   ║                                 ║ │
        │   ║  [SERVER]      [SERVER]       ║ │
        │   ║                                 ║ │
        │   ╚═════════════════════════════════╝ │
        │                                       │
        ├───────────────────────────────────────┤
        │                                       │
        │   [MAIN EXIT]                        │
        │   [→ Tầng 18]                       │
        │   (Sau khi hạ Bullwork)             │
        │                                       │
        │   [EVIDENCE ROOM]                   │
        │   [L:Legendary - Prometheus data]   │
        │   [Mission 14 reward]                │
        │                                       │
        └───────────────────────────────────────┘
```

## 7.6 Zombie Distribution

| Tầng | Loại | Số lượng | Ghi chú |
|---|---|---|---|
| Tầng 1 | Security | 1 | Reception |
| Tầng 1 | Security | 2 | Security desk |
| Tầng 2-14 | Walker | 2/tầng | Cubicle + meeting room |
| Tầng 2-14 | Walker | 1/tầng | Kitchenette |
| Tầng 15 | Security | 2 | Hallway |
| Tầng 18 | Security | 1 | Utility building |
| Tầng Hầm 4 | **BULLWORK (Boss)** | 1 | Boss arena |

---

# PHẦN VIII — SCENE 6: HARBOR

**Tên Scene:** Harbor
**Kích thước:** 300×200m
**Chức năng:** Act 4 — Lãnh thổ Blackout, zombie nhiều nhất
**Tone:** Mặn, dầu, container, cảng công nghiệp

## 8.1 Layout tổng quan

```
                    [BẾN CẢNG — HARBOR]
                    ═══════════════════
                         │
    ┌────────────────────┼────────────────────┐
    │                    │                    │
    │   [KHO HÀNG A]     │   [KHO HÀNG B]    │
    │   (Container x20)   │   (Container x20) │
    │   [Blackout Camp]  │   [Z:x8 Walker]   │
    │   [Shadow spawn]   │   [L:Uncm x5]     │
    │                    │                    │
    ├────────────────────┼────────────────────┤
    │                    │                    │
    │   [CẦU CẢNG]      │   [TÀU "AURORA"]  │
    │   ═══════════      │   ═══════════════  │
    │   [Snipe point]    │   [L:Rare x3]     │
    │   [Z:x4 Runner]    │   [Brute x1]      │
    │   [Blackout sniper]│   [Evidence]      │
    │                    │                    │
    ├────────────────────┼────────────────────┤
    │                    │                    │
    │   [ĐƯỜNG CHÍNH]   │   [KHO CŨ]       │
    │   ════════════════ │   ════════════   │
    │                    │   [Zombie x6]     │
    │   [Z:x10 Horde]   │   [Loot x3]       │
    │   (Horde trigger) │                   │
    │                    │                   │
    ├────────────────────┴────────────────────┤
    │                                          │
    │   [VĂN PHÒNG CẢNG]                       │
    │   ══════════════════════                 │
    │   [MAP - reveal Eastside]                │
    │   [Z:x2 Walker]                          │
    │   [NPC: Survivor - wounded]              │
    │                                          │
    ├──────────────────────────────────────────┤
    │                                          │
    │         [ĐƯỜNG RA — EASTSIDE]           │
    │         [→ Eastside Portal]              │
    │         [Blackout ambush x4]             │
    │                                          │
    └──────────────────────────────────────────┘
```

## 8.2 Chi tiết từng khu vực

### KHU A — KHO HÀNG A (Container Yard A)

```
        KHO HÀNG A (100×80m)
        ═════════════════════════════

        [╔═══╗][╔═══╗][╔═══╗][╔═══╗][╔═══╗]
        [║ C ║][║ C ║][║ C ║][║ C ║][║ C ║]
        [╚═══╝][╚═══╝][╚═══╝][╚═══╝][╚═══╝]
             [C] = Container (có thể trèo)

        ─────────────────────────────────────

        [C1]  [C2]  [C3]  [C4]  [C5]  [C6]
         │     │     │     │     │     │
         │     │     │     │     │     │
        [Z1]  [Z2] [LOOT] [Z3]  │    [Z4]
         ☠     ☠    (Ammo) ☠     │     ☠
                                 │
                                [C7]
                                (Blackout Camp)
                                [SHADOW REYES]
                                [Henchman x2]
                                [Quest: SQ6]

        [C8]  [C9]  [C10] [C11] [C12]
         │     │     │     │     │
        [Cvr] │    [Cvr]  │    [Cvr]
              │           │         │
             [Z5]       [Z6]      [Loot]
              ☠           ☠      (Medkit)
```

- **SHADOW REYES:** Boss encounter (SQ6: Trả thù)
- **BLACKOUT CAMP:** Trong container lớn, có supplies
- **SNIPER:** Blackout sniper trên nóc kho hàng

### KHU B — CẦU CẢNG (Pier)

```
        CẦU CẢNG (150×20m)
        ═══════════════════════════════════

        [WATER — không thể bơi (infected water)]
        ════════════════════════════════════════

        ┌──────────────────────────────────────────────┐
        │           CẦU CẢNG                           │
        │    ════════════════════════════════════       │
        │                                              │
        │    [RAILING - có thể phá]                   │
        │                                              │
        │   [ZOMBIE x4]                               │
        │    ☠  ☠  ☠  ☠                               │
        │   (Runner - lao nhanh)                      │
        │                                              │
        │         [SNIPER POINT]                      │
        │         (Trên container cao)                 │
        │         [BLACKOUT SNIPER]                    │
        │         "Đừng tiến lên, lính."              │
        │                                              │
        │   ════════════════════════════════════════  │
        │                                              │
        │              [TÀU AURORA]                   │
        │              ════════════════               │
        │              [Brute x1]                     │
        │              [L:Rare x3]                    │
        │              [Ship log - lore]              │
        │                                              │
        └──────────────────────────────────────────────┘
```

### KHU C — TÀU AURORA (MS Aurora)

```
        TÀU "AURORA" (60×30m)
        ═════════════════════════════

        SÀN CHÍNH (Main Deck)
        ┌─────────────────────────────────────┐
        │                                      │
        │   [BRIDGE]                          │
        │   [Captain body + log]              │
        │   [L:Rare - Ship manifest]          │
        │   [Zombie: Brute x1]                │
        │                                      │
        │   ════════════════════════════════   │
        │                                      │
        │   [CARGO HOLD]                      │
        │   [Container x10]                   │
        │   [Zombie x6 Walker]                │
        │   [L:Uncommon x5]                   │
        │   [L:Rare x1 - grenade launcher]    │
        │   (Prototype - lore item)           │
        │                                      │
        │   [CREW QUARTERS]                   │
        │   [Zombie x2]                       │
        │   [L:Cmn x2]                        │
        │                                      │
        └─────────────────────────────────────┘
```

## 8.3 Zombie Distribution

| Khu vực | Loại | Số lượng | Trigger |
|---|---|---|---|
| Kho A | Walker | 8 | Khi vào kho |
| Kho A | Runner | 2 | Khi đến Blackout camp |
| Cầu cảng | Runner | 4 | Khi bước lên cầu |
| Tàu Aurora | Brute | 1 | Khi vào tàu |
| Tàu Aurora | Walker | 6 | Khi vào cargo hold |
| Tàu Aurora | Walker | 2 | Crew quarters |
| Đường chính | Walker | 10 | Horde trigger |
| Kho cũ | Walker | 6 | Khi vào kho |
| Văn phòng cảng | Walker | 2 | Khi vào văn phòng |
| Blackout ambush | Human | 4 | Khi ra về |

---

# PHẦN IX — SCENE 7: EASTSIDE

**Tên Scene:** Eastside
**Kích thước:** 150×150m
**Chức năng:** Act 4 — Khu vực Sarah, kết thúc
**Tone:** Yên tĩnh hơn, personal, stealth

## 9.1 Layout tổng quan

```
                         [ĐƯỜNG RA]
                    ═══════════════════
                         │
    ┌──────────────────┼──────────────────┐
    │                  │                  │
    │  ┌──────────┐    │    ┌──────────┐  │
    │  │ CONG VIEN │    │    │ SCHOOL   │  │
    │  │ (Park)   │    │    │  MẪU    │  │
    │  │──────────│    │    │  GIÁO   │  │
    │  │ [Z:x2]  │    │    │──────────│  │
    │  │ [L:Cmn]│    │    │ [Z:x1]  │  │
    │  │ [Kid]  │    │    │ [Lily]  │  │
    │  │ swings │    │    │ (body)  │  │
    │  └──────────┘    │    └──────────┘  │
    │                  │                  │
    │     ┌────────────┼────────────┐     │
    │     │            │            │     │
    │     │   KHU NHÀ  │  PHỐ       │     │
    │     │   ─────── │            │     │
    │     │   ┌───┐    │  ┌───┐    │     │
    │     │   │H1 │    │  │H2 │    │     │
    │     │   │   │    │  │   │    │     │
    │     │   │[L]│    │  │[Z]│    │     │
    │     │   └───┘    │  └───┘    │     │
    │     │            │           │     │
    │     │ [H3]       │    [H4]  │     │
    │     │  (Sarah's │    │(Blackout│     │
    │     │   house) │    │ camp) │     │
    │     │  [Loot]  │    │[Z:x4] │     │
    │     │  [Sarah] │    │      │     │
    │     │  [Lily]  │    │      │     │
    │     │  [Safe]  │    │      │     │
    │     │  [NPC]   │    │      │     │
    │     └───────────┘    └───────┘     │
    │                  │                  │
    └──────────────────┼──────────────────┘
                       │
                  [→ Hub Portal]
```

## 9.2 Chi tiết khu vực

### KHU A — NHÀ SARAH (Sarah's House)

```
        MẶT BẰNG NHÀ (20×15m)
        ═════════════════════════════

        TẦNG 1
        ┌─────────────────────────────────┐
        │                                 │
        │   [PHÒNG KHÁCH]                │
        │   ════════════════════         │
        │   [Sofa]                       │
        │   [Photo frame - Marcus+Sarah] │
        │   [Graffiti: "We survived"]    │
        │                                 │
        │   [KITCHEN]                    │
        │   [Empty fridge]               │
        │   [Supply: very low]          │
        │                                 │
        ├─────────────────────────────────┤
        │                                 │
        │   [HALLWAY]                     │
        │        │                        │
        │        ▼                        │
        │   [BATHROOM]                    │
        │   [Blood on floor]             │
        │   (Whose blood?)               │
        │                                 │
        │        │                        │
        │        ▼                        │
        │   [LILY'S ROOM]                 │
        │   [Toys]                       │
        │   [Drawings]                   │
        │   [Safe - hidden]              │
        │   [Code: 734] (hint: 7+3+4)    │
        │   [L:Legendary - Medkit]       │
        │                                 │
        │        │                        │
        │        ▼                        │
        │   [SARAH'S ROOM]               │
        │   [Bed - unmade]              │
        │   [Letter to Marcus]           │
        │   [Journal entry]              │
        │                                 │
        └─────────────────────────────────┘
```

- **BLOOD:** Có vết máu trong phòng tắm — dù Sarah hay Lily?
- **SAFE:** Ẩn sau tranh, mở bằng code 734
- **LETTER:** Sarah viết cho Marcus — tiết lộ nhiều điều

### KHU B — CONG VIEN (Park)

```
        CÔNG VIÊN (60×40m)
        ═════════════════════════════

        ┌───────────────────────────────────────┐
        │                                        │
        │        [BENCH x3]                      │
        │        ══════════════════             │
        │                                        │
        │   [SWING]    [SWING]   [SLIDE]        │
        │    (đung đưa    (đung đưa)            │
        │     một mình)    (bình thường)         │
        │                                        │
        │   ════════════════════════════════    │
        │                                        │
        │        [FOUNTAIN - khô cạn]           │
        │        (Có xác ở đáy)                │
        │        [Zombie x2 - Walker]            │
        │                                        │
        │   [TREES x10]                          │
        │   (Có thể cover)                       │
        │   [Ammo x10 - under tree]              │
        │                                        │
        └───────────────────────────────────────┘
```

### KHU C — BLACKOUT CAMP

```
        BLACKOUT CAMP (40×40m)
        ═════════════════════════════

        ┌─────────────────────────────────┐
        │                                  │
        │   [CONTAINER - HQ]              │
        │   ════════════════════         │
        │   [Shadow's gang x4]           │
        │   [Armory]                     │
        │   [L:Rare - weapon]            │
        │                                  │
        ├─────────────────────────────────┤
        │                                  │
        │   [FIRE PIT]                    │
        │   ═══════════                   │
        │   [Smoke signal]                │
        │   (Có thể thấy từ Hub)         │
        │                                  │
        │   [ZOMBIE x4]                   │
        │   (Bị Blackout dùng làm rào)   │
        │                                  │
        │   [COVER: car wrecks]          │
        │                                  │
        └─────────────────────────────────┘
```

## 9.3 Zombie Distribution

| Khu vực | Loại | Số lượng | Trigger |
|---|---|---|---|
| Công viên | Walker | 2 | Khi vào công viên |
| Nhà H2 | Walker | 1 | Khi vào nhà |
| Blackout camp | Walker | 4 | Khi đến gần |
| Sarah's house | 0 | 0 | Không zombie — safe zone |

---

# PHẦN X — SCENE 8: EVACUATION POINT

**Tên Scene:** EvacuationPoint
**Kích thước:** 50×50m, trên nóc tòa nhà chính quyền
**Chức năng:** Endgame — Wave cuối cùng, kết thúc
**Tone:** Căng thẳng, đỉnh điểm, hy vọng

## 10.1 Layout

```
        SÂN THƯỢNG — EVACUATION POINT (50×50m)
        ═══════════════════════════════════════════════

        ╔════════════════════════════════════════════╗
        ║                                            ║
        ║              HELIPAD                       ║
        ║           ════════════════                 ║
        ║           ║   [HELICOPTER]  ║             ║
        ║           ║   (Đang đến)    ║             ║
        ║           ║   [ELENA wait]  ║             ║
        ║           ╚═════════════════╝             ║
        ║                                            ║
        ║     ══════════════════════════════════     ║
        ║                                            ║
        ║   [WATER TOWER]      [ANTENNA]           ║
        ║   (Cover - sniper)   (Cover - sniper)    ║
        ║                                            ║
        ╠════════════════════════════════════════════╣
        ║                                            ║
        ║            WAVE DEFENSE ZONE               ║
        ║         ════════════════════════            ║
        ║                                            ║
        ║     [COVER: car wrecks x4]                ║
        ║     [COVER: sandbag x8]                   ║
        ║     [COVER: barrier x6]                   ║
        ║                                            ║
        ║   [ZOMBIE WAVE 1: x10 Walker]            ║
        ║   [ZOMBIE WAVE 2: x8 Walker + x4 Runner]  ║
        ║   [ZOMBIE WAVE 3: x10 + x6 + x2 Crawler] ║
        ║   [ZOMBIE WAVE 4: x15 + x8 + x4 + Brute] ║
        ║   [ZOMBIE WAVE 5: ALL + BRUTE x2]        ║
        ║                                            ║
        ╠════════════════════════════════════════════╣
        ║                                            ║
        ║   [STAIRWELL EXIT]                         ║
        ║   [→ Eastside Portal]                      ║
        ║   (Chỉ mở sau wave 3)                      ║
        ║                                            ║
        ╚════════════════════════════════════════════╝
```

## 10.2 Wave System

| Wave | Zombie | Số lượng | Spawn |
|---|---|---|---|
| 1 | Walker | 10 | Từ cầu thang |
| 2 | Walker + Runner | 8 + 4 | Từ cầu thang + 2 phía |
| 3 | Walker + Runner + Crawler | 10 + 6 + 2 | Từ mọi hướng |
| 4 | Walker + Runner + Crawler + Brute | 15 + 8 + 4 + 1 | Từ mọi hướng |
| 5 (Final) | ALL + Brute x2 | 20 + 10 + 6 + 2 | Final wave |

- **Thời gian giữa wave:** 10 giây
- **Trực thăng đến:** Sau wave 5, đợi 5 giây
- **Hết thời gian:** Nếu HP < 0 → Game Over → Restart wave 5

## 10.3 Kết thúc

```
        CUTSCENE — KẾT THÚC
        ═══════════════════════════

        Trực thăng đáp xuống. Tất cả người sống sót lên.

        ┌───────────────────────────────────────┐
        │                                        │
        │   WIDE SHOT: Helipad + thành phố       │
        │   (Greenlake đang bị bao vây)          │
        │                                        │
        │   FADE TO BLACK...                     │
        │                                        │
        │   TEXT:                                │
        │   "Ngày 52 sau Ngày 0"                 │
        │   "Trực thăng rời Greenlake"           │
        │   "Khoảng 40 người được cứu"           │
        │   "Helena Cross vẫn ở tầng hầm"        │
        │   "Prometheus-7 vẫn còn tồn tại"        │
        │                                        │
        │   Tùy thuộc vào lựa chọn của bạn:       │
        │                                        │
        │   Kết thúc A: Sarah không có mặt        │
        │   Kết thúc B: James Park đã chết       │
        │   Kết thúc C: Ai lên trực thăng?       │
        │                                        │
        │   "DEAD ZONE SURVIVAL"                  │
        │   "Cảm ơn bạn đã chơi"                 │
        │   "THE END"                             │
        │                                        │
        └───────────────────────────────────────┘
```

---

# PHẦN XI — HỆ THỐNG LOADING SCENE

## 11.1 Loading Screen Design

```
        ┌───────────────────────────────────────┐
        │                                        │
        │                                        │
        │                                        │
        │          [LOGO: Dead Zone]            │
        │                                        │
        │          Đang rời khỏi:               │
        │          [Old Town]                    │
        │                                        │
        │          ════════════════             │
        │                                        │
        │          ████████░░░░░░  67%          │
        │                                        │
        │                                        │
        │   "Ngày 48 sau Ngày 0"                │
        │   "Thành phố đã im lặng..."           │
        │                                        │
        │                                        │
        └───────────────────────────────────────┘
```

## 11.2 Transition Rules

| Từ | Đến | Thời gian | Loại |
|---|---|---|---|
| MainMenu | Hub | 2s | Fade black |
| Hub | OldTown | 2s | Fade black |
| OldTown | Hub | 2s | Fade black |
| OldTown | Northside | 2s | Fade black |
| Northside | Hospital | 2s | Fade black |
| Hospital | Mall | 2s | Fade black |
| Hospital | HelixTower | 2s | Fade black |
| Mall | Harbor | 2s | Fade black |
| Harbor | Eastside | 2s | Fade black |
| Eastside | Hub | 2s | Fade black |
| Eastside | Evacuation | 2s | Fade black |
| Any | GameOver | 1s | Fade red |

## 11.3 Code cho Scene Transition

```csharp
public class SceneTransitionManager : MonoBehaviour
{
    public static SceneTransitionManager Instance;

    [SerializeField] private Image fadeImage;
    [SerializeField] private Text loadingText;
    [SerializeField] private Slider loadingSlider;

    void Start()
    {
        Instance = this;
        fadeImage.gameObject.SetActive(true);
        // Start: fade in
        fadeImage.color = Color.black;
        fadeImage.canvasRenderer.SetAlpha(1f);
        fadeImage.CrossFadeAlpha(0f, 1f, false);
    }

    public void TransitionToScene(string sceneName, string fromLocation)
    {
        StartCoroutine(TransitionCoroutine(sceneName, fromLocation));
    }

    IEnumerator TransitionCoroutine(string sceneName, string fromLocation)
    {
        // Fade out (0.5s)
        fadeImage.gameObject.SetActive(true);
        fadeImage.CrossFadeAlpha(1f, 0.5f, false);
        loadingText.text = $"Đang rời khỏi: {fromLocation}";
        loadingSlider.gameObject.SetActive(true);

        yield return new WaitForSeconds(0.5f);

        // Load scene async
        AsyncOperation op = SceneManager.LoadSceneAsync(sceneName);
        op.allowSceneActivation = false;

        while (!op.isDone)
        {
            loadingSlider.value = op.progress;
            yield return null;
        }

        // Small delay
        yield return new WaitForSeconds(0.5f);

        // Fade in (0.5s)
        fadeImage.CrossFadeAlpha(0f, 0.5f, false);
        loadingSlider.gameObject.SetActive(false);

        yield return new WaitForSeconds(0.5f);
        fadeImage.gameObject.SetActive(false);
    }
}
```

---

# PHẦN XII — BẢNG TỔNG HỢP MỌI SCENE

## 12.1 Thông tin tổng hợp

| Scene | Kích thước | Tầng | Safe? | Zombie tối đa | Loot tier |
|---|---|---|---|---|---|
| Hub_FireStation | 80×80m | 2 | ✅ | 0 | Common-Rare |
| Tutorial_OldTown | 150×150m | 1 | ❌ | 15 | Common-Rare |
| Northside | 200×200m | 1 | ❌ | 25 | Common-Uncommon |
| Hospital | 60×60m | 9 | ❌ | 30 | Uncommon-Rare |
| Mall | 120×120m | 4 | ❌ | 40 | Common-Legendary |
| HelixTower | 40×40m | 22 | ❌ | 25 | Rare-Epic |
| Harbor | 300×200m | 1 | ❌ | 35 | Uncommon-Rare |
| Eastside | 150×150m | 2 | ⚠️ | 10 | Common-Rare |
| EvacuationPoint | 50×50m | 1 | ❌ | 50 (wave) | — |

## 12.2 Bảng Portal

| ID | Scene hiện tại | Vị trí | Đến Scene | Spawn position |
|---|---|---|---|---|
| P_1 | Hub | Cửa lớn | Tutorial_OldTown | Start House |
| P_2 | Tutorial | Cổng ra | Hub | Hub entrance |
| P_3 | Hub | Cửa sườn | Northside | Northside entrance |
| P_4 | Northside | Đại lộ | Hospital | Hospital entrance |
| P_5 | Northside | Đường ra | Eastside | Eastside entrance |
| P_6 | Hospital | Cửa chính | Hub | Hub entrance |
| P_7 | Hospital | Thang hầm | HelixTower | Helix basement |
| P_8 | Mall | Emergency exit | Northside | Northside edge |
| P_9 | Mall | Loading dock | Harbor | Harbor entrance |
| P_10 | HelixTower | Lobby | Mall | Mall edge |
| P_11 | Harbor | Đường ra | Eastside | Eastside entrance |
| P_12 | Eastside | Đường ra | Hub | Hub entrance |
| P_13 | Eastside | Đường ra | EvacuationPoint | Evac rooftop |

---

*Tài liệu Phiên bản: 1.0*
*Ngày cập nhật: 03/05/2026*
*Hướng dẫn Layout Map Chi tiết*
