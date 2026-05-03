# Huong Dan Su Dung Map Generation Tools

Huong dan su dung cac cong cu map generation da duoc tich hop vao project.

---

## Muc Luc
1. [TTG - Terrain Generation](#1-ttg---terrain-generation)
2. [ProceduralStructures - Tao Cong Trinh](#2-proceduralstructures---tao-cong-trinh)
3. [Cigen - Layout Thanh Pho](#3-cigen---layout-thanh-pho)
4. [CityGenerator-Unity - Tao Thanh Pho](#4-citygenerator-unity---tao-thanh-pho)
5. [ProBuilder - Xay Dung Map Tay](#5-probuilder---xay-dung-map-tay)
6. [Cac Asset Can Tai Them](#6-cac-asset-can-tai-them)

---

## 1. TTG - Terrain Generation

**Duong dan**: `Assets/TTG/`
**Cong dung**: Tao terrain map procedural (dat, nuoc, dac diem dia hinh)

### Cach su dung:
1. Mo Unity, vao **Window > TTG > Terrain Generator**
2. Chon kich thuoc terrain (Width, Height, Length)
3. Dat seed neu can (de co the tao lai cung terrain)
4. Chon he so nhieu (Noise Scale) cho dia hinh
5. Chon chieu cao (Height Scale)
6. Click **Generate** de tao terrain
7. Sau khi tao xong, terrain nam trong Scene

### Cac tuy chon:
- **Noise Scale** nho = dia hinh binh on hon, **lon** = gap guoc hon
- **Height Scale** chinh do cao cua terrain
- **Seed** = 0 nghia la random moi lan

### Lenh truc tiep (neu can):
```
Window > TTG > Terrain Generator
```

---

## 2. ProceduralStructures - Tao Cong Trinh

**Duong dan**: `Assets/ProceduralStructures/`
**Cong dung**: Tao cac cong trinh procedural (nha cua, tuong, cau thang, vuong)

### Cach su dung:
1. Vao **Window > Procedural Structures**
2. Chon loai structure muon tao:
   - **Tower**: Thap
   - **Wall**: Tuong
   - **Stairs**: Cau thang
   - **Courtyard**: San vuon
   - **Random**: Ngau nhien
3. Thiet lap cac thong so (chieu cao, rong, so tang)
4. Click **Generate** hoac **Generate in Scene**
5. Object duoc tao trong Scene

### Tuy chon chinh:
- **Floor Count**: So tang
- **Room Size**: Kich thuoc phong
- **Seed**: Seed cho random

---

## 3. Cigen - Layout Thanh Pho

**Duong dan**: `Assets/Cigen/`
**Cong dung**: Tao layout thanh pho procedural (duong, khu vuc)

### Cach su dung:
1. Vao **Assets > Cigen > Editor**
2. Dat kich thuoc city (Grid Size)
3. Chon mat do (Density): thua thom, trung binh, day dun
4. Chon loai duong (Road Type): Grid, Organic, Hybrid
5. Click **Generate**
6. Layout duong xuat hien trong Scene

### Lenh menu:
```
Assets > Cigen > Generate City Layout
```

---

## 4. CityGenerator-Unity - Tao Thanh Pho

**Duong dan**: `Assets/CityGenerator-Unity/`
**Cong dung**: Tao thanh pho procedural day du (toan can ho, mat bieu, nha o)

### Cach su dung:
1. Trong Scene, tao object moi: **Create Empty**
2. Attach script **CityGenerator.cs** vao object do
3. Trong Inspector, thiet lap:
   - **Grid Size**: Kich thuoc luoi thanh pho
   - **Block Size**: Kich thuoc moi block
   - **Building Count**: So luong toa nha
   - **Seed**: Seed random
4. Click **Generate City** trong Inspector

### Hoac qua menu:
```
GameObject > City Generator > Generate City
```

### Tuy chon chinh:
- **Max Building Height**: Chieu cao toi da toa nha
- **Min Building Height**: Chieu cao toi thieu
- **Building Gap**: Khoang cach giua cac toa nha
- **Use Roads**: Co danh duong hay khong

---

## 5. ProBuilder - Xay Dung Map Tay

**Cong dung**: Xay dung map truc tiep trong Unity (da cai san)

### Cach su dung:
1. Vao **Tools > ProBuilder > ProBuilder Window**
2. Chon shape muon tao:
   - **Stairs**: Cau thang
   - **Cube**: Hop
   - **Cylinder**: Hinh tru
   - **Door**: Cua
   - **Pillar**: Cot
   - **Roof**: Mai nha
   - **Tube**: Ong
   - **Arch**: Von cua
3. Click **Shape** de tao object trong Scene
4. Edit bang cach:
   - **Enter Edit Mode**: Double-click vao object
   - Di chuyen, xoa, them **Vertex** (dinh), **Edge** (canh), **Face** (mat)
   - **Extrude Face**: Keo dai mat
   - **Inset Face**: Thu nho mat
   - **Bridge Edge**: Noi 2 canh
5. Ra khoi Edit Mode: Nhan **Ctrl+B**

### Phim tat:
| Phim | Chuc nang |
|---|---|
| `Shift + Click` | Chon nhieu |
| `Ctrl + Click` | Them / Bo chon |
| `D` | Duplicate |
| `G` | Grid Snap |
| `Ctrl + Shift + F` | Can chinh camera |
| `Backspace` | Xoa da chon |
| `F` | Focus vao object |

### Cac cong cu ProBuilder:
- **Vertex**: Di chuyen tung diem
- **Edge**: Xoay, di chuyen canh
- **Face**: Extrude, inset, di chuyen mat
- **UV Editor**: Chinh UV cho texture
- **Material Palette**: Dat material cho mat

---

## 6. Cac Asset Can Tai Them

Day la cac asset **FREE** can tai tu Asset Store de ho tro tao map:

### 6.1 Terrain & Landforms

#### Polaris 2 - Low Poly Terrain Engine
- **Link**: https://assetstore.unity.com/packages/tools/terrain/polaris-2-low-poly-terrain-engine-170042
- **Cong dung**: Thay the terrain mac dinh, tao terrain low-poly dep mat, co he thong paint, smooth valley, river
- **Huong dan**:
  1. Tai tu Asset Store
  2. Import vao project
  3. Vao **Window > Poloris 2 > Terrain Editor**
  4. Ve terrain bang cac brush (bristle, noise, smooth, ridge)

#### Terrain Former
- **Link**: https://assetstore.unity.com/packages/tools/terrain/terrain-former-141518
- **Cong dung**: Chinh sua terrain bang brush, tao rac, tao hien tuong tu nhien
- **Huong dan**:
  1. Tai + Import
  2. Chon terrain object
  3. Vao **Terrain > Terrain Former**

### 6.2 Buildings & Props

#### Snaps Prototype
- **Link**: https://assetstore.unity.com/packages/3d/props/snaps-prototype-87869
- **Cong dung**: Bo do gach, thanh pho, van phong, nha cu, gia dung (FREE)
- **Huong dan**:
  1. Tai + Import
  2. Keo prefabs tu **Assets > Snaps Prototypes** vao Scene
  3. Su dung Snaps Object **Snap to Grid** de xep dat

#### Free Low Poly Desert Pack
- **Link**: https://assetstore.unity.com/packages/3d/environments/landscapes/free-low-poly-desert-pack-55579
- **Cong dung**: Dac san, cat, doi da cho vung sa mac

#### Free Low Poly Nature Kit
- **Link**: https://assetstore.unity.com/packages/3d/environments/freelowpoly-nature-kit-138736
- **Cong dung**: Cay coi, hoa, co, go, da cho vung nhiet doi

### 6.3 Dungeon

#### Dungeon Architect
- **Link**: https://assetstore.unity.com/packages/tools/modeling/dungeon-architect-52898
- **Cong dung**: Tu dong tao dungeon layout voi nhieu style (medieval, sci-fi, cave)
- **Huong dan**:
  1. Tai + Import
  2. Vao **Dungeon > Dungeon Architect**
  3. Chon theme (medieval, sci-fi, cave, modular)
  4. Click **Build Dungeon**
  5. Ket noi voi Snaps Prototype de tao dungeon day du

### 6.4 Map Generation

#### Map Graph
- **Link**: https://assetstore.unity.com/packages/tools/terrain/map-graph-procedural-world-generator-268553
- **Cong dung**: Tao world map procedural, tao heightmap, tao texture terrain tu graph
- **Huong dan**:
  1. Tai + Import
  2. Vao **Window > Map Graph**
  3. Tao graph moi, them cac node (Noise, Biome, Layer, etc.)
  4. Ket noi node de tao world
  5. Click **Generate**

---

## Quy Trinh Tao Map Day Du (De Quy)

```
1. TAO TERRAIN (TTG hoac Polaris 2)
   └── Window > TTG > Terrain Generator > Generate

2. TAO LAYOUT THANH PHO (Cigen)
   └── Assets > Cigen > Generate City Layout

3. TAO TOA NHA (CityGenerator-Unity)
   └── Tao object > Attach CityGenerator > Generate City

4. TAO CONG TRINH PHU (ProceduralStructures)
   └── Window > Procedural Structures > Chon type > Generate

5. DAT PROPS (Snaps + Nature kits)
   └── Keo prefabs tu Assets > Snaps Prototypes vao Scene

6. CHINH SUA & XAY DUNG (ProBuilder)
   └── Tools > ProBuilder > ProBuilder Window > Ve / Chinh sua

7. DAT RA (Dungeon Architect - neu can dungeon)
   └── Dungeon > Dungeon Architect > Build Dungeon

8. HOAN THIEN (ProBuilder + Manual editing)
   └── Xay tuong, cau, duong, noi cac block lai voi nhau
```

---

## Ghi Chu Quan Trong

1. **Backup** truoc khi generate: Ctrl+S thuong xuyen
2. **Save scene** moi sau khi tao map
3. **ProBuilder** la cong cu chinh de hoan thien map - cac tool kia chi tao base
4. **HDRP** da duoc setup san - chi can dat materials len object
5. **NavMesh**: Sau khi xay xong map, vao **Window > AI > Navigation** de bake NavMesh cho zombie di chuyen
6. **Lighting**: Vao **Lighting > Scene** de bake GI cho map

---

## Tro Ly

Neu gap loi:
- **ProceduralStructures loi**: Kiem tra Unity version (can 2021.3+)
- **Cigen loi**: Co the can Editor scripts - vao **Assets > Cigen** de kiem tra
- **HDRP materials loi**: Click **Edit > Render Pipeline > Upgrade Project Materials to HDRP**
- **NavMesh khong bake**: Dam bao tat ca static geometry deu danh dau **Navigation Static**
