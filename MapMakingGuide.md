# HƯỚNG DẪN CÔNG CỤ & TÀI NGUYÊN LÀM MAP
## Dead Zone Survival — Map Making Guide v1.0

---

# PHẦN I — TỔNG QUAN CHIẾN LƯỢC MAP

## 1.1 Mô hình map được chọn: Hub-Scene Open World

```
                    [BẾN CẢNG - HARBOR]
                          │
                    [KHU CÔNG NGHIỆP]
                    ─────────────────
                         │
  [KHU Ổ CHUỘT]──[ĐẠI LỘ TRUNG TÂM]──[KHU TÀI CHÍNH]
       │                │                    │
  [NHÀ MÁY CŨ]    [TRUNG TÂM THƯƠNG MẠI]   [TRỤ SỞ HELIX]
       │                │                    │
  [KHU DÂN CƯ]    [KHU DÂN CƯ PHÍA BẮC]   [BỆNH VIỆN ST.MARGARET]
                      │                    │
        [KHU PHỐ CỔ - OLD TOWN]────────[TRẠM CỨU HỎA #7]
               │                    │
         [KHU DÂN CƯ]          [KHU ĐÔNG - EASTSIDE]
          (Start)               (Sarah's area)

Điểm sơ cua (Endgame): [HELIPAD - ROOFTOP]
```

**Đặc điểm:**
- **8 scene riêng biệt**, kết nối qua portal/trigger
- Mỗi scene load độc lập → performance tốt cho co-op
- Hub (Fire Station #7) là điểm trung tâm — người chơi quay về giữa các nhiệm vụ
- Loading screen có cinematic fade (2s) giữa các scene
- Tổng diện tích khám phá: ~1-2 km²

## 1.2 Scene List

| # | Tên Scene | Kích thước | Thời gian load ước tính | Ghi chú |
|---|---|---|---|---|
| 0 | **MainMenu** | — | — | Menu chính |
| 1 | **Hub_FireStation** | 80×80m | < 1s | Safe zone, không zombie |
| 2 | **Tutorial_OldTown** | 150×150m | 2-3s | Tutorial, Act 1 |
| 3 | **Northside** | 200×200m | 2-3s | Act 1-2 |
| 4 | **Hospital** | 60×60m, 8 tầng | 2s | Act 2 |
| 5 | **Mall** | 120×120m, 3 tầng | 3s | Act 2-3 |
| 6 | **HelixTower** | 40×40m, 18 tầng | 3s | Act 3 |
| 7 | **Harbor** | 300×200m | 3-4s | Act 4 |
| 8 | **Eastside** | 150×150m | 2s | Act 4, Kết thúc |
| 9 | **EvacuationPoint** | 50×50m | < 1s | Wave cuối, Endgame |

**Thứ tự chơi:** Hub → Tutorial → Northside → Hospital ↔ Mall ↔ HelixTower → Harbor ↔ Eastside → EvacuationPoint

---

# PHẦN II — TERRAIN & ĐỊA HÌNH (FREE)

## 2.1 MapMagic 2 — Tạo terrain vô hạn

**Link:** https://assetstore.unity.com/packages/tools/terrain/mapmagic-2-165180
**Giá:** **FREE**
**License:** Unity Asset Store Standard

### Giới thiệu
MapMagic 2 là procedural terrain generator mạnh nhất cho Unity. Tạo địa hình (đồi, núi, thung lũng, sông) bằng node-based graph. Hoàn toàn miễn phí.

### Tính năng chính
- Infinite terrain (vô hạn terrain)
- Node-based workflow — kéo thả node tạo terrain
- Noise-based heightmap (Perlin, Simplex, Voronoi...)
- Biome system — mỗi khu vực có texture riêng
- Hỗ trợ URP, HDRP, Built-in
- Chunk-based loading — chỉ load terrain trong tầm nhìn
- Đã test với Unity 2021-2023

### Cách dùng cơ bản

```
Bước 1: Window → Package Manager → Tìm "MapMagic 2" → Import
Bước 2: GameObject → Create Other → MapMagic → Tạo MapMagic object
Bước 3: Trong Inspector, thêm node:
         Output > Output Tile
         ↓
         Input > Noise > (chỉnh frequency, octaves)
         ↓
         Output > Texture > (chọn texture: dirt, grass, rock)
Bước 4: Play → Terrain tự sinh ra theo noise
Bước 5: Chỉnh MapMagic radius = 500 (cho map 1km×1km)
```

### Node Graph mẫu cho Old Town

```
[Noise: frequency=0.01, octaves=4] → [Curve: flatten center]
        ↓
[Output Tile: 512×512, height=50]
        ↓
[Texture: blend grass/dirt/sand theo height]
```

### Module mở rộng (tùy chọn)

| Module | Giá | Chức năng |
|---|---|---|
| MapMagic 2 Objects | ~$20 | Đặt object procedural (cây, đá, nhà) |
| MapMagic 2 Roads | ~$15 | Tạo đường tự động |
| MapMagic 2 Core | **FREE** | Đã đủ cho basic terrain |

## 2.2 Terrain Tools — Built-in

**Link:** Đã có trong Unity (Window → Package Manager → Terrain Tools)
**Giá:** **FREE**

### Giới thiệu
Công cụ chỉnh terrain thủ công. Dùng để tinh chỉnh terrain do MapMagic tạo ra hoặc vẽ terrain từ đầu.

### Tính năng
- **Raise/Lower Terrain** — cào nâng hạ địa hình
- **Smooth Terrain** — làm mịn
- **Paint Texture** — phủ texture (cỏ, đất, đá, bùn)
- **Place Trees** — đặt cây (dùng kèm vegetation asset)
- **Paint Details** — thêm cỏ, bụi (dùng kèm vegetation)
- **Terrain Settings** — chỉnh resolution, heightmap

### Cách dùng

```
Bước 1: Chọn terrain object trong scene
Bước 2: Window → Package Manager → Terrain Tools → Import
Bước 3: Terrain → Terrain Toolbox (trong menu) để mở panel
Bước 4: Dùng brush để chỉnh heightmap
         - Di chuột để raise/lower
         - Shift+chuột để smooth
         - Ctrl+chuột để flatten
Bước 5: Terrain Layers → Add Layer → Import texture cho từng lớp
         - Layer 0: Grass (cỏ) - low height
         - Layer 1: Dirt (đất) - mid height
         - Layer 2: Rock (đá) - high height
```

## 2.3 Gaia 2021 — Terrain + Vegetation

**Link:** https://assetstore.unity.com/packages/tools/terrain/gaia-2021-pro-247186
**Giá:** **FREE**

### Giới thiệu
Gaia là terrain generator + vegetation system. Tự động tạo cảnh quan hoàn chỉnh: terrain + cây + cỏ + nước + đá. Đặc biệt hữu ích cho khu vực Harbor và khu công nghiệp.

### Tính năng
- **Terrain Generation** — tạo terrain tự động
- **Procedural Vegetation** — đặt cây, cỏ, bụi theo rule
- **Water System** — tạo sông, hồ, biển
- **Wind Zones** — cỏ lay động theo gió
- **Biome Masking** — phân chia khu vực theo biome
- ** Stamper** — stamp địa hình (vẽ núi, hẻm)

### Cách dùng

```
Bước 1: Window → Gaia → Bootstrap Gaia → Create World
Bước 2: Chọn "Default" world profile
Bước 3: Terrain Generator → Generate Terrain
         - Resolution: 513×513
         - Height: 600
         - Width: 2000
Bước 4: Terrain Texture → Apply Texture Pro
         - Chọn texture set (Grasslands, Forest...)
Bước 5: Spawn Trees → Spawn
         - Density: 1000
         - Chọn tree prototype
Bước 6: Spawn Grass → Spawn
         - Density: 10000
         - Chọn grass prototype
```

## 2.4 TTG — Terraced Terrain Generator

**Link:** https://github.com/lazysquirrellabs/TTG
**Giá:** **FREE (MIT License)**

### Giới thiệu
Terrain generator đơn giản, tạo terrain kiểu "bậc thang" (terraced). Phù hợp cho khu vực đồi núi hoặc khu công nghiệp.

### Tính năng
- Planar và spherical terrain
- Synchronous và asynchronous generation
- Customizable terraces, size, height
- Unity Package Manager compatible

### Cách cài đặt

```
Bước 1: Unity → Window → Package Manager → Add from GitHub
Bước 2: Nhập: https://github.com/lazysquirrellabs/TTG.git
Bước 3: Import vào project
Bước 4: GameObject → Create Other → TTG → Terraced Terrain
Bước 5: Chỉnh parameters:
         - Width: 100
         - Height: 20
         - Terrace Count: 10
         - Noise Intensity: 0.3
```

---

# PHẦN III — THÀNH PHỐ & NHÀ CỬA (FREE)

## 3.1 ProceduralStructures — Tạo nhà procedural

**Link:** https://github.com/nothingTVatYT/ProceduralStructures
**Giá:** **FREE (MIT License)**

### Giới thiệu
Tạo nhà và thành phố procedural. Đặt đường đi (waypoint) → nó sinh nhà theo đường đó. Dùng cho Old Town, Northside, Eastside.

### Tính năng
- Procedural house generation — nhà có thể 1-5 tầng
- Window, door, balcony procedural
- Street generation — đường đi tự tạo
- Roof styles — nhiều kiểu mái (flat, gable, hip)
- Material variety — nhiều texture ngẫu nhiên
- Unity 2020+ compatible

### Cách dùng

```
Bước 1: Clone/GitHub → Download ZIP → Import vào Unity
Bước 2: GameObject → Create Other → ProceduralStructures → City Generator
Bước 3: Trong CityGenerator component:
         - Number of Buildings: 50
         - Min Floors: 1, Max Floors: 5
         - Street Width: 10
         - Building Width: 8-20
Bước 4: Nhấn "Generate City"
Bước 5: Đợi vài giây → thành phố procedural xuất hiện
Bước 6: Tinh chỉnh bằng ProBuilder nếu cần
```

### Workflow cho Old Town

```
1. Dùng ProceduralStructures tạo base (nhà + đường)
2. Dùng ProBuilder chỉnh sửa từng nhà:
   - Thêm chi tiết: cửa sổ vỡ, graffiti
   - Thêm indoor space: phòng ngủ, phòng khách
   - Đặt furniture: giường, bàn, ghế (dùng Low Poly Pack)
3. Đặt spawn point cho zombie trong nhà
4. Đặt loot spawner ở tầng 1 và tầng 2
```

## 3.2 Cigen — Tạo đường + tòa nhà procedural

**Link:** https://github.com/gregoryneal/Cigen
**Giá:** **FREE (MIT License)**

### Giới thiệu
Cigen tập trung vào tạo **đường xá + tòa nhà** procedural. Dùng thuật toán anisotropic least cost pathfinder để đặt đường tự nhiên như thật.

### Tính năng
- Road placement algorithm thông minh
- Tự động đặt building dọc theo đường
- Configurable building height (high-rise, low-rise)
- Grid-based và organic street patterns
- MIT License — dùng thoải mái cho commercial

### Cách dùng

```
Bước 1: Clone/GitHub → Import vào Unity
Bước 2: GameObject → Create Other → Cigen → City Generator
Bước 3: Setup:
         - Map Size: 500×500
         - Road Density: 0.3
         - Building Density: 0.6
         - Height Variation: High
Bước 4: Generate → City xuất hiện
```

## 3.3 CityGenerator-Unity — Cityscape procedural

**Link:** https://github.com/Szuszi/CityGenerator-Unity
**Giá:** **FREE (MIT License)**

### Giới thiệu
Tạo cityscape procedural với high-rise và low-rise. Có tutorial YouTube. Dùng cho khu tài chính (Helix Tower area).

### Tính năng
- Perlin noise cho phân bố high-rise/low-rise
- Streets với randomly spawned benches
- Parks với trees
- Positional variance cho organic look

## 3.4 ProceduralCity — City procedural đơn giản

**Link:** https://github.com/jackwhelan/ProceduralCity
**Giá:** **FREE**

### Giới thiệu
City generator đơn giản, dùng Perlin noise. Phù hợp cho prototype nhanh.

### Tính năng
- High-rise và low-rise areas
- Streets với benches
- Parks với trees
- Configurable noise parameters

---

# PHẦN IV — PROBUILDER — CHỈNH SỬA MAP THỦ CÔNG

## 4.1 ProBuilder — Built-in

**Link:** Window → Package Manager → ProBuilder (đã có sẵn)
**Giá:** **FREE (Built-in Unity)**

### Giới thiệu
ProBuilder là công cụ **vẽ và chỉnh sửa geometry trực tiếp trong Unity**. Không cần 3D software bên ngoài. Dùng để tạo mọi thứ: nhà, cầu, tường, nội thất.

### Tính năng
- **Vertex editing** — kéo đỉnh, cạnh, mặt
- **Polybrush** — sơn vertex color, texture
- **Face editing** — thêm, xóa, extrude mặt
- **Shape tool** — tạo hình có sẵn (stair, cylinder, arch)
- **UV Editing** — chỉnh UV cho texture
- **Procedural shapes** — tạo cầu thang, vòm, ống dẫn

### Lệnh cơ bản

| Hành động | Cách làm |
|---|---|
| Chọn ProBuilder | Window → Package Manager → ProBuilder → Import |
| Tạo hình mới | GameObject → ProBuilder → Shape → Chọn shape |
| Vào Edit Mode | Double-click object hoặc nhấn Ctrl+Shift+E |
| Extrude face | Chọn face → Alt+E |
| Bevel edge | Chọn edge → Ctrl+B |
| Flip normals | Tooltip → Flip Face Direction |
| Tạo window | Tạo hình vuông → Extrude → Flip normals → Texture window |
| Tạo cầu thang | GameObject → ProBuilder → Stair |

### Cách dùng cho khu vực Helix Tower

```
Bước 1: Tạo 1 box làm base (40×40×72m — 18 tầng × 4m)
Bước 2: Vào Edit Mode → Flip normals để nhìn từ trong ra
Bước 3: Thêm floor (tạo box mới, scale 40×0.3×40, đặt ở mỗi 4m)
Bước 4: Thêm cầu thang: GameObject → ProBuilder → Stair → Đặt 2 bên
Bước 5: Thêm cửa: Tạo cube nhỏ ở vị trí cửa → Subtract (bool) để cắt lỗ
Bước 6: UV unwrap → Apply texture (glass, concrete)
Bước 7: Thêm chi tiết: desk, chair, computer → Low Poly Pack
```

### Kinh nghiệm ProBuilder

**1. Quy tắc khi vẽ nhà cho zombie game:**
```
- Mỗi phòng có ÍT NHẤT 1 cửa ra vào (zombie có thể vào)
- Cửa sổ có thể là lối vào cho Crawler
- Hành lang hẹp = chỗ zombie đuổi người chơi
- Phòng lớn = chỗ combat wave
- Có nhiều đường thoát = người chơi không kẹt
```

**2. Layout cơ bản cho 1 ngôi nhà:**

```
┌──────────────────────┐
│  PHÒNG NGỦ  │  PHÒNG NGỦ  │
│    (Loot 1)  │    (Loot 2)  │
│      [S]      │      [S]      │
└───────┬──────┴──────────────┘
        │
┌───────┴───────┐
│              │
│  HÀNH LANG   │
│              │
│     [D]      │  ← Door
└───────┬──────┘
        │
┌───────┴───────┐
│              │
│  PHÒNG KHÁCH  │
│    (Spawn Z)  │
│      [Z]      │
└──────────────┘
   [F] ← Front door
```

**3. Material workflow:**
```
- Base: Concrete Wall (texture từ Nature Starter Kit)
- Detail: Cracked concrete overlay
- Blood: Decal (dùng Decal Projector)
- Breakable: Tạo prefab với BreakableObject.cs
```

---

# PHẦN V — ASSET PACK MIỄN PHÍ (FREE)

## 5.1 Vegetation & Nature

### Nature Starter Kit 2
**Link:** https://assetstore.unity.com/packages/3d/vegetation/nature-nature-nature-starter-kit-2-52977
**Giá:** **FREE**

Bao gồm: 60 loại cây, 50 loại cỏ, 20 loại đá, 30 loại bụi cây. Đủ cho khu vực ngoài trời.

### Low Poly Free Pack (OG 24 Models)
**Link:** https://assetstore.unity.com/packages/3d/models/low-poly-free-pack-og-24-models-55524
**Giá:** **FREE**

24 model low-poly: cây, đá, xe, nhà, xe hơi, xe tải, cây cối. Dùng cho prototype hoặc game low-poly style.

### Free Starter Assets — Trees
**Link:** https://assetstore.unity.com/packages/3d/vegetation/trees/free-starter-stylized-trees-152六
**Giá:** **FREE**

Stylized trees — phù hợp cho game không quá realistic.

### SpeedTree for Unity
**Link:** https://assetstore.unity.com/packages/tools/speedtree-for-unity-109445
**Giá:** **FREE**

SpeedTree là engine vegetation chuyên nghiệp. Version miễn phí có 10 cây.

## 5.2 Props & Props Pack

### Free Street Props
**Link:** https://assetstore.unity.com/packages/3d/props/exterior/free-street-props-139674
**Giá:** **FREE**

Bao gồm: băng đá, thùng rác, ghế đá, biển báo giao thông, lamp post, barrier, fence. Dùng cho khu dân cư và đường phố.

### Free Cottage Kit
**Link:** https://assetstore.unity.com/packages/3d/props/interior/free-cottage-kit-194748
**Giá:** **FREE**

Props cho nội thất nhà: giường, bàn, ghế, tủ, kệ sách, đèn, tranh.

### Free Medical Props
**Link:** https://assetstore.unity.com/packages/3d/props/free-medical-props-24678
**Giá:** **FREE**

Props cho bệnh viện: giường bệnh, máy MRI, bình oxy, xe đẩy, khuôn, băng.

### Post Apocalyptic Props Pack
**Link:** https://assetstore.unity.com/packages/3d/props/exterior/post-apocalyptic-props-pack-136086
**Giá:** **FREE**

Props apocalpse: xe hỏng, container, thùng phuy, pallet, xác xe, barricade. **RẤT PHÙ HỢP** cho zombie game.

### Crates & Barrels
**Link:** https://assetstore.unity.com/packages/3d/props/exterior/crates-barrels-55062
**Giá:** **FREE**

Thùng gỗ, thùng kim loại, pallet. Dùng làm cover trong combat + loot spawner.

### Sci-Fi Industrial Modular Pack
**Link:** https://assetstore.unity.com/packages/3d/models/industrial/sci-fi-industrial-modular-pack-free-204574
**Giá:** **FREE**

Props công nghiệp: ống dẫn, van, bảng điều khiển, cáp. Dùng cho Helix Tower và Harbor.

## 5.3 Characters & Humanoids

### Unity Starter Assets — FPS (QUAN TRỌNG NHẤT)
**Link:** https://assetstore.unity.com/packages/templates/starter-assets-first-person-character-controller-177326
**Giá:** **FREE**

**ĐÂY LÀ ASSET BẮT BUỘC PHẢI CÓ.** Bao gồm:
- First Person Controller (WASD + jump + sprint + crouch)
- Third Person Controller
- Mobile touch controls
- Input system ready
- Physics-based movement

```
Cách cài đặt:
1. Unity Asset Store → Tìm "Starter Assets"
2. Download → Import vào project
3. Scene nào cần FPS → thêm "PlayerArms" prefab
4. Thêm FirstPersonController vào scene
5. Play → đã có thể di chuyển + ngắm + bắn
```

### Zombie Humanoid Male
**Link:** https://assetstore.unity.com/packages/3d/characters/humanoids/zombie/zombie-humanoid-male-free-150409
**Giá:** **FREE**

1 zombie male humanoid. Đủ để test.

### Zombie Simple Characters Pack
**Link:** https://assetstore.unity.com/packages/3d/characters/humanoids/zombie-simple-characters-pack-190784
**Giá:** **FREE**

4 zombie humanoid: male, female, child, brute.

### Modern Weapons Pack — FREE Version
**Link:** https://assetstore.unity.com/packages/3d/weapons/modern-weapons-pack-free-157748
**Giá:** **FREE**

6 vũ khí free: M4, M1911, AK47, Shotgun, Sniper, Grenade. Không có anim, chỉ model.

### Free Weapons Pack
**Link:** https://assetstore.unity.com/packages/3d/weapons/free-weapons-pack-204631
**Giá:** **FREE**

20 vũ khí: knife, pistol, SMG, rifle, shotgun. Không có anim.

## 5.4 Effects & Particles

### Unity Particle Pack
**Link:** https://assetstore.unity.com/packages/vfx/particles/unity-particle-pack-127620
**Giá:** **FREE**

50+ particle effect: lửa, khói, bụi, máu, nước, ma thuật. **Dùng cho muzzle flash, blood splatter, explosion.**

### FX Mega Pack — FREE
**Link:** https://assetstore.unity.com/packages/vfx/particles/fx-mega-pack-free-215046
**Giá:** **FREE**

Effects cho combat: muzzle flash, bullet impact, blood, fire, explosion, debris.

### Free Smoke & Fog Particles
**Link:** https://assetstore.unity.com/packages/vfx/particles/free-smoke-fog-particles-191315
**Giá:** **FREE**

Smoke và fog particles. Dùng cho atmosphere: khói từ đống đổ nát, sương mù buổi sáng.

## 5.5 Audio — Âm thanh miễn phí

### Zombie / Horror SFX Pack
**Link:** https://assetstore.unity.com/packages/audio/sound-effects-zombies/zombie-sound-effects-pack-free-144374
**Giá:** **FREE**

Âm thanh zombie: tiếng gầm, tiếng bước chân, tiếng tấn công.

### Free Sound Effects Pack
**Link:** https://assetstore.unity.com/packages/audio/sound-effects/free-sound-effects-pack-184371
**Giá:** **FREE**

Âm thanh môi trường: tiếng gió, tiếng mưa, tiếng đổ vỡ, tiếng cửa.

### Free Gun Sound Pack
**Link:** https://assetstore.unity.com/packages/audio/sound-effects/free-gun-sound-pack-154342
**Giá:** **FREE**

Âm thanh súng: bắn, nạp, đạn trúng.

---

# PHẦN VI — TERRAIN DECORATION & ATMOSPHERE

## 6.1 Free Grass & Flowers Pack
**Link:** https://assetstore.unity.com/packages/3d/vegetation/trees/free-grass-and-flowers-pack-142342
**Giá:** **FREE**

50 loại cỏ và hoa. Dùng cho terrain ngoài trời.

## 6.2 Rocks and Boulders Pack
**Link:** https://assetstore.unity.com/packages/3d/vegetation/rocks/free-rocks-and-boulders-pack-121665
**Giá:** **FREE**

Đá và Boulder. Dùng cho khu công nghiệp, bến cảng.

## 6.3 Skybox — Free

### Deep Sky
**Link:** https://assetstore.unity.com/packages/vfx/shaders/free-deep-sky-standalone-38692
**Giá:** **FREE**

8 skybox: nắng, mây, hoàng hôn, đêm, bão. **Dùng cho thời gian trong ngày.**

### Free Low Poly Skyboxes
**Link:** https://assetstore.unity.com/packages/vfx/shaders/free-low-poly-skyboxes-126329
**Giá:** **FREE**

Low poly style skybox. Phù hợp với Low Poly Free Pack.

## 6.4 Decal

### Decal Massive Runtime Pack
**Link:** https://assetstore.unity.com/packages/vfx/shaders/decal/decalmassive-runtime-pack-120812
**Giá:** **FREE**

Decal: blood splatter, graffiti, burn mark, crack. Dùng phủ khắp map để tăng detail.

### Free Blood Decals
**Link:** https://assetstore.unity.com/packages/vfx/particles/free-blood-decals-pack-162342
**Giá:** **FREE**

Blood decal. Rất quan trọng cho zombie game.

---

# PHẦN VII — NAVIGATION & AI

## 7.1 Unity NavMesh — Built-in

**Link:** Window → AI → Navigation (đã có sẵn)
**Giá:** **FREE**

Unity NavMesh là hệ thống pathfinding có sẵn. Dùng cho zombie AI.

### Cách dùng

```
Bước 1: Đánh dấu tất cả ground = Navigation Static
         (Chọn ground → Inspector → Navigation Static ✓)
Bước 2: Window → AI → Navigation → Bake
Bước 3: Bake Settings:
         - Agent Radius: 0.5 (zombie size)
         - Agent Height: 2 (zombie height)
         - Max Slope: 45 (zombie có thể leo)
         - Step Height: 0.75 (zombie có thể bước lên)
Bước 4: Nhấn Bake → NavMesh được tạo
Bước 5: Zombie prefab → Thêm NavMeshAgent component
Bước 6: Trong script: agent.SetDestination(player.position)
```

### Cài đặt cho từng loại zombie

| Zombie | Agent Radius | Agent Speed | Step Height |
|---|---|---|---|
| Walker | 0.5 | 2 | 0.4 |
| Runner | 0.4 | 6 | 0.4 |
| Crawler | 0.3 | 4 | 0.1 |
| Brute | 1.0 | 1.5 | 0.2 |
| Screamer | 0.5 | 3 | 0.4 |

## 7.2 A* Pathfinding Project (bản có phí)

**Link:** https://assetstore.unity.com/packages/tools/ai/a-pathfinding-project-urp-hdrp-18788
**Giá:** ~$60 (bản free có giới hạn)

### Khi nào cần?
- Khi Unity NavMesh không đủ (dynamic obstacles)
- Khi zombie cần nhảy, leo, bơi
- Khi cần multi-agent avoidance phức tạp

### Khuyến nghị
**BẮT ĐẦU với Unity NavMesh có sẵn.** Upgrade lên A* Pathfinding Project khi:
- Game đã chơi được
- Cần tính năng advanced (dynamic navmesh, multiple agents)

---

# PHẦN VIII — LIGHTING & POST PROCESSING

## 8.1 Lighting (Built-in + Free)

### Post Processing Stack v2
**Link:** Window → Package Manager → Post Processing
**Giá:** **FREE**

Tất cả effects: bloom, color grading, vignette, motion blur, ambient occlusion. **BẮT BUỘC PHẢI CÓ** cho atmosphere.

### Cách setup

```
Bước 1: Install Post Processing từ Package Manager
Bước 2: Tạo Volume: GameObject → Volume → Global Volume
Bước 3: Thêm Post-process Layer vào Main Camera
         - Layer: Post Processing
Bước 4: Trong Volume → Add Override → Post Processing
         - Bloom: intensity 0.5 (cho đêm)
         - Color Grading: Night look (cool blue)
         - Vignette: intensity 0.4 (tăng tension)
         - Chromatic Aberration: small (kinh nghiệm)
```

### Atmosphere Setup cho zombie game

| Thời gian | Ambient | Sun | Fog | Post FX |
|---|---|---|---|---|
| **Ngày** | Blue-ish | Strong, warm | Light | Saturated |
| **Hoàng hôn** | Orange | Medium | Medium | Warm tint |
| **Đêm** | Dark blue | None | Heavy | Dark, desaturated, bloom on lights |

### Lighting Optimization cho FPS

```
1. GIỚI HẠN số light source trong scene:
   - Max 1 Directional Light (sun/moon)
   - Max 10 Point Lights (chiếu sáng trong nhà)
   - Max 5 Spot Lights (player flashlight)

2. DÙNG baked lighting:
   - Realtime GIời tốn nhiều FPS
   - Baked GIời tốn RAM nhưng không tốn FPS
   - Kết hợp: Baked ambient + Realtime directional

3. LIGHT PROBE:
   - Đặt Light Probe Group xung quanh map
   - Moving objects (player, zombie) dùng probe để nhận lighting
   - Tiết kiệm performance
```

## 8.2 Dynamic Lighting — Free

### URP (Universal Render Pipeline)
**Link:** Window → Package Manager → Universal RP
**Giá:** **FREE**

URP là render pipeline mới của Unity. Nhanh hơn Built-in, đẹp hơn, miễn phí.

**Ưu điểm:**
- HDRP (bản cao cấp) miễn phí cho Unity 2022+
- Shader graph tích hợp
- Shader được tối ưu sẵn
- Post processing dễ setup

### HDRP (High Definition Render Pipeline)
**Link:** Window → Package Manager → HDRP
**Giá:** **FREE**

Cho ai muốn đồ họa đẹp nhất. Yêu cầu máy mạnh hơn.

---

# PHẦN IX — CO-OP NETWORKING

## 9.1 Mirror — Open Source Networking

**Link:** https://assetstore.unity.com/packages/tools/network/mirror-8158
**Link GitHub:** https://github.com/MirrorNetworking/Mirror
**Giá:** **FREE (MIT License)**

### Giới thiệu
Mirror là networking library mạnh nhất cho Unity. Dùng bởi hàng triệu game. MIT license — dùng cho commercial thoải mái.

### Tính năng

| Tính năng | Hỗ trợ |
|---|---|
| Server/Client architecture | ✅ |
| Host game (P2P) | ✅ |
| Dedicated server | ✅ |
| Unity Relay (free 100GB/tháng) | ✅ |
| Steam integration | ✅ |
| RPC (Remote Procedure Call) | ✅ |
| SyncVar (đồng bộ biến) | ✅ |
| NetworkIdentity | ✅ |
| Scene management | ✅ |
| Physics prediction | ✅ |
| Interest management | ✅ |

### Setup cơ bản

```
Bước 1: Unity Asset Store → Tải Mirror → Import
Bước 2: Window → Mirror → Setup Wizard
Bước 3: Chọn "Add Network Manager to Scene"
Bước 4: Đánh dấu Player prefab = NetworkIdentity
         - Player.prefab → Add Component → NetworkIdentity
         - Player.prefab → Add Component → NetworkTransform
Bước 5: Trong NetworkManager:
         - Registered Spawnable Prefabs → Thêm Player prefab
         - Player Prefab → Thêm Player prefab
Bước 6: Thêm NetworkManagerHUD (built-in UI) để test
Bước 7: Play → Server: "Host" | Client: "Connect"
```

### Sync Code mẫu

```csharp
// Sync Player Position
public class NetworkPlayer : NetworkBehaviour
{
    [SyncVar] private Vector3 position;
    [SyncVar] private Quaternion rotation;

    void Update()
    {
        if (isLocalPlayer)
        {
            // Send position to server
            CmdMove(transform.position, transform.rotation);
        }
        else
        {
            // Update from server
            transform.position = position;
            transform.rotation = rotation;
        }
    }

    [Command]
    void CmdMove(Vector3 pos, Quaternion rot)
    {
        position = pos;
        rotation = rot;
    }
}
```

### Multi-Scene với Mirror

```csharp
// Khi người chơi đi qua portal
public class ScenePortal : MonoBehaviour
{
    public string targetScene;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            if (isServer)
            {
                // Server quyết định chuyển scene
                NetworkManager.singleton.ServerChangeScene(targetScene);
            }
        }
    }
}
```

## 9.2 Unity Relay — Server miễn phí

**Link:** https://dashboard.unity3d.com/relay
**Giá:** **FREE 100GB/tháng**

Unity Relay cho phép người chơi kết nối qua server của Unity, không cần mở port hay dùng Hamachi.

```
Cách kích hoạt:
1. Unity Dashboard → Services → Relay → Enable
2. Trong Unity: Window → Package Manager → Relay
3. Trong Mirror: NetworkManager → Transport → Unity Relay Transport
4. Tạo Relay allocation từ code:
   Allocation allocation = await RelayService.CreateAllocationAsync(4);
   JoinAllocation join = await RelayService.JoinAllocationAsync(allocationId);
   // Share joinCode với bạn bè
```

## 9.3 So sánh Networking Options

| Tính năng | Mirror | PUN2 | Netcode for GameObjects |
|---|---|---|---|
| Chi phí | **FREE** | **FREE** (20CCU) | **FREE** |
| Dedicated server | ✅ | ❌ | ✅ |
| Steam | ✅ | ❌ | ✅ |
| Unity Relay | ✅ | ✅ | ✅ |
| Physics sync | ✅ | ✅ | ✅ |
| Scene management | ✅ | ✅ | ✅ |
| Migration (host leave) | ✅ | ✅ | ❌ |
| Documentation | Tốt | Tốt | Trung bình |
| Active development | ✅ (2026) | LTS only | ✅ |
| Game nào dùng | Nhiều indie game | Mobile game | Unity samples |

**Kết luận:** Dùng **Mirror** cho game này.

---

# PHẦN X — WORKFLOW TỔNG HỢP

## 10.1 Quy trình làm 1 map (từ đầu đến cuối)

### Ngày 1-2: Terrain + Layout

```
1. Mở Unity → Tạo scene mới "Scene_OldTown"
2. Thêm Terrain (100×100m):
   - Terrain → Terrain Settings → Resolution: 513×513
   - Dùng MapMagic 2 hoặc Gaia để generate terrain
   - Hoặc dùng Terrain Tools vẽ thủ công
3. Thêm Ground Plane (nếu cần):
   - GameObject → 3D Object → Plane
   - Scale: 150×150
4. Đặt directional light (sun):
   - Directional Light → Rotation để có ánh sáng đẹp
5. Đặt skybox:
   - Lighting Settings → Skybox → Chọn Deep Skybox
6. Setup NavMesh:
   - Đánh dấu Terrain = Navigation Static
   - Window → AI → Navigation → Bake
   - Radius: 0.5, Height: 2, Step: 0.4
```

### Ngày 3-4: Nhà cửa + Đường phố

```
1. Dùng ProceduralStructures hoặc Cigen tạo base city
2. ProBuilder chỉnh sửa:
   - Sửa từng building (thêm chi tiết, cửa, cửa sổ)
   - Tạo indoor space cho zombie spawn
   - Thêm cover objects (xe hỏng, thùng rác, barrier)
3. Import Free Asset Pack:
   - Low Poly Free Pack → thêm xe, đá, cây
   - Free Street Props → thêm băng đá, biển báo
   - Crates & Barrels → thêm cover cho combat
4. Đặt Decal (blood, graffiti):
   - Decal Massive Runtime Pack → đặt khắp map
5. Kiểm tra NavMesh:
   - Test bằng cách đặt 1 zombie và chạy thử
```

### Ngày 5: Props + Chi tiết

```
1. Thêm nội thất trong nhà:
   - Free Cottage Kit → giường, bàn, ghế
   - Free Medical Props → cho khu Hospital
2. Thêm atmosphere:
   - Particle Pack → khói, bụi (Settings: Fog Volume)
   - Free Smoke → đặt quanh đống đổ nát
3. Thêm điểm tham quan:
   - Journal entry (tạo prefab đơn giản)
   - Audio log trigger (tạo prefab đơn giản)
4. Đặt spawn point cho zombie:
   - Empty GameObject đánh dấu vị trí
   - Ghi vào script WaveManager
5. Đặt loot spawner:
   - Empty GameObject + LootSpawner.cs
   - Config tier (Common, Uncommon, Rare)
```

### Ngày 6: Lighting + Post FX + Polish

```
1. Setup lighting:
   - Directional Light (sun): Baking = Mixed, Intensity 1
   - Point Lights (trong nhà): Baking = Baked, Range 10
   - Light Probes: Đặt xung quanh map
2. Setup Post Processing:
   - Volume → Post Process Layer (camera)
   - Bloom: intensity 0.3 (nhẹ)
   - Color Grading: Look -2 (giảm saturation cho zombie game)
   - Vignette: intensity 0.3
   - Depth of Field: chỉ khi ngắm súng
3. Fog:
   - Lighting → Fog: Color gray, Density 0.01
4. Audio:
   - Audio Source cho ambient (gió, khung cảnh)
   - Đặt trong nhà: echo/reverb
5. Final test:
   - Chạy FPS movement → kiểm tra framerate
   - Kiểm tra NavMesh → zombie có đi được hết không
   - Kiểm tra Loot → item spawn đúng tier chưa
```

## 10.2 Bảng checklist cho mỗi scene

| # | Hạng mục | Check |
|---|---|---|
| 1 | Terrain + Ground | ☐ |
| 2 | Skybox + Lighting | ☐ |
| 3 | NavMesh baked | ☐ |
| 4 | Building procedural | ☐ |
| 5 | Building edited (ProBuilder) | ☐ |
| 6 | Props placed | ☐ |
| 7 | Decal applied | ☐ |
| 8 | Indoor space defined | ☐ |
| 9 | Zombie spawn points | ☐ |
| 10 | Loot spawn points | ☐ |
| 11 | Journal/Audio log | ☐ |
| 12 | Portal/Exit trigger | ☐ |
| 13 | Post Processing | ☐ |
| 14 | Audio (ambient) | ☐ |
| 15 | Fog | ☐ |
| 16 | FPS test (movement) | ☐ |
| 17 | FPS test (60fps target) | ☐ |
| 18 | Network test (Mirror) | ☐ |

---

# PHẦN XI — BẢNG TỔNG HỢP TOOLS

## 11.1 FREE — Bắt buộc

| Tool | Link | Dùng cho | Ưu tiên |
|---|---|---|---|
| **Unity 2022 LTS** | unity.com/download | Nền tảng | ⭐⭐⭐ |
| **FPS Starter Assets** | Asset Store | Movement + bắn | ⭐⭐⭐ |
| **Mirror** | Asset Store / GitHub | Co-op networking | ⭐⭐⭐ |
| **MapMagic 2** | Asset Store | Terrain generation | ⭐⭐⭐ |
| **ProBuilder** | Package Manager (built-in) | Map editing | ⭐⭐⭐ |
| **Terrain Tools** | Package Manager (built-in) | Terrain editing | ⭐⭐ |
| **Unity Post Processing** | Package Manager (built-in) | Graphics effects | ⭐⭐ |
| **Unity NavMesh** | Window → AI → Navigation | Zombie AI pathfinding | ⭐⭐ |
| **ProceduralStructures** | GitHub (MIT) | City procedural | ⭐⭐ |
| **Cigen** | GitHub (MIT) | Road procedural | ⭐ |
| **Low Poly Free Pack** | Asset Store | Props | ⭐⭐ |
| **Nature Starter Kit 2** | Asset Store | Vegetation | ⭐⭐ |
| **Free Street Props** | Asset Store | Street props | ⭐⭐ |
| **Unity Particle Pack** | Asset Store | Effects | ⭐ |
| **Post Apocalyptic Props** | Asset Store | Zombie atmosphere | ⭐⭐ |
| **Free Blood Decals** | Asset Store | Blood effect | ⭐ |
| **Deep Skybox** | Asset Store | Sky/atmosphere | ⭐ |

## 11.2 RẺ — Nên mua (~$60-100)

| Tool | Giá ước | Dùng cho | Thay thế free |
|---|---|---|---|
| **Dungeon Architect** | ~$60 | Auto-generate layout (mall, harbor) | ProBuilder thủ công |
| **Gaia 2021** | ~$40 (FREE version có) | Terrain + vegetation nâng cao | Terrain Tools |
| **Low Poly Zombie Pack** | ~$20 | Nhiều zombie hơn | Free zombie pack |
| **Modular City Kit** | ~$50 | Nhà modular đẹp | ProceduralStructures |

## 11.3 LỘ TRÌNH MUA ASSET

```
TUẦN 1-4:  Chỉ dùng FREE (test prototype)
TUẦN 5-8:  Mua Dungeon Architect (~$60) — cho Mall + Harbor layout
TUẦN 9-12: Mua Low Poly Zombie Pack (~$20) — nhiều zombie hơn
TUẦN 13+:  Mua Modular City Kit (~$50) — nếu cần map đẹp hơn
```

---

# PHẦN XII — TRÁNH CÁC LỖI THƯỜNG GẶP

## Lỗi 1: NavMesh không bake được
```
Nguyên nhân: Object chưa đánh dấu Navigation Static
Giải pháp: Chọn object → Inspector → Navigation Static ✓
```

## Lỗi 2: Zombie đi xuyên tường
```
Nguyên nhân: Collider không match với mesh
Giải pháp: Kiểm tra collider size trong NavMeshAgent
            - Agent Radius phải nhỏ hơn door width
            - Agent Height phải đúng với zombie height
```

## Lỗi 3: FPS drop khi có nhiều zombie
```
Nguyên nhân: Quá nhiều AI tính toán mỗi frame
Giải pháp:
1. Object Pooling — reuse zombie thay vì spawn/destroy
2. Frustum culling — zombie ngoài camera không update AI
3. Distance culling — zombie xa 100m chỉ update position, không update AI
4. Batch rendering — dùng GPU Instancing cho zombie giống nhau
```

## Lỗi 4: Map load quá lâu
```
Nguyên nhân: Quá nhiều object trong scene
Giải pháp:
1. Dùng addressables để load object theo nhu cầu
2. Bật "Optimize Game Objects" trong FBX import
3. Đặt object không bao giờ nhìn thấy = None (no render)
4. Dùng LOD cho model xa
```

## Lỗi 5: Lighting không đẹp
```
Nguyên nhân: Chưa setup GI (Global Illumination)
Giải pháp:
1. Window → Rendering → Lighting
2. Lighting Settings → Auto Generate = OFF
3. Nhấn Generate Lighting (đợi 5-10 phút)
4. Dùng Baked GI (không phải Realtime GI)
```

---

# PHẦN XIII — THAM KHẢO

## YouTube Tutorial

| Video | Link | Nội dung |
|---|---|---|
| MapMagic 2 Tutorial | Tìm "MapMagic 2 tutorial" trên YouTube | Hướng dẫn setup + node graph |
| ProBuilder Basics | Tìm "ProBuilder tutorial Unity" | Cách vẽ map |
| Mirror FPS Tutorial | Tìm "Mirror networking Unity FPS" | Setup co-op |
| Procedural City | Tìm "Cigen Unity tutorial" | City generation |
| Zombie AI Unity | Tìm "Unity NavMesh zombie AI" | AI setup |

## Documentation

| Tài liệu | Link |
|---|---|
| Unity Manual | docs.unity3d.com |
| MapMagic Docs | Có trong asset sau khi import |
| Mirror Docs | mirror-networking.gitbook.io |
| ProBuilder Docs | docs.unity3d.com/Packages/probuilder |

---

*Tài liệu Phiên bản: 1.0*
*Ngày cập nhật: 03/05/2026*
*Hướng dẫn Map Making Tools*
