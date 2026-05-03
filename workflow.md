# Zombie Survival - Unity Project Workflow

## Project Setup

- **Unity Version**: 6000.4.5f1
- **Render Pipeline**: HDRP (High Definition Render Pipeline)
- **Platform Target**: PC (Windows) | Multiplayer

---

## Package Dependencies

### Da cai san (co san trong manifest.json)
| Package | Version | Purpose |
|---|---|---|
| com.unity.collab-proxy | 2.12.4 | Unity Collab |
| com.unity.feature.development | 1.0.2 | Dev tools (Profiler, etc) |
| com.unity.inputsystem | 1.19.0 | New Input System |
| com.unity.multiplayer.center | 1.0.1 | Multiplayer |
| com.unity.render-pipelines.high-definition | 17.4.0 | HDRP |
| com.unity.timeline | 1.8.12 | Timeline/Cutscenes |
| com.unity.ugui | 2.0.0 | UI |
| com.unity.visualscripting | 1.9.11 | Visual Scripting (Bolt) |
| com.unity.probuilder | 6.0.9 | Map building tool |
| com.unity.terrain-tools | 5.0.4 | Terrain editing |
| com.unity.ai.navigation | 2.0.5 | NavMesh AI |

### Can tai tay (Asset Store / GitHub)
**TU TAI (Asset Store - Free)**:
- [Polaris 2 - Low Poly Terrain Engine](https://assetstore.unity.com/packages/tools/terrain/polaris-2-low-poly-terrain-engine-170042) - Thay the cho terrain-tools, generate terrain procedural
- [Map Graph](https://assetstore.unity.com/packages/tools/terrain/map-graph-procedural-world-generator-268553) - Procedural map generation
- [Dungeon Architect](https://assetstore.unity.com/packages/tools/modeling/dungeon-architect-52898) - Dungeon layout generator
- [Ruins of the-Fallen](https://assetstore.unity.com/packages/templates/ruins-of-the-fallen-244266) - Environment props
- [Terrain Former](https://assetstore.unity.com/packages/tools/terrain/terrain-former-141518) - Brush-based terrain shaping
- [QuickEdit - Polybrush](https://assetstore.unity.com/packages/tools/modeling/polybrush-111309) - Mesh painting/edit
- [Snaps Prototyping](https://assetstore.unity.com/packages/3d/props/snaps-prototype-87869) - Building assets (free)
- [Free Low Poly Desert Pack](https://assetstore.unity.com/packages/3d/environments/landscapes/free-low-poly-desert-pack-55579) - Environment
- [Free Low Poly Nature Kit](https://assetstore.unity.com/packages/3d/environments/freelowpoly-nature-kit-138736) - Nature props
- [Zombie Mega Pack](https://assetstore.unity.com/packages/3d/characters/humanoids/zombie-mega-pack-120507) - Zombie models
- [Character Pack: Zombie Sample](https://assetstore.unity.com/packages/3d/characters/humanoids/character-pack-zombie-sample-40078) - Zombie model
- [Post Processing Stack v2](https://assetstore.unity.com/packages/essentials/post-processing-stack-83913) - Da co san roi (HDRP co Post Processing)

**Da clone tu GitHub (trong Assets/)**:
| Repo | Source | Purpose |
|---|---|---|
| Assets/ProceduralStructures | github.com/nothingTVatYT/ProceduralStructures | Generate building/structures |
| Assets/Cigen | github.com/gregoryneal/Cigen | Procedural city layout |
| Assets/ProceduralCity | github.com/jackwhelan/ProceduralCity | Procedural city generation |
| Assets/TTG | github.com/lazysquirrellabs/TTG | Terrain generation |
| Assets/CityGenerator-Unity | github.com/Szuszi/CityGenerator-Unity | City building generator |

---

## Folder Structure

```
Assets/
  Animations/          # Animator controllers, animation clips
  Audio/               # Music, SFX, Voice
    Music/
    SFX/
    Voice/
  Materials/           # HDRP Materials
  Models/              # 3D models (FBX)
  Prefabs/             # Prefabs
    Player/
    Zombie/
    Weapons/
    Items/
    UI/
  Resources/           # Resources.Load
  Scenes/              # Unity scenes
  Scripts/             # C# scripts
    Player/
    Zombie/
    AI/
    Game/
    UI/
    Network/
    Scene/
    Misc/
    Weapons/
    Items/
    Interaction/
  Textures/            # Textures, normal maps
  ProceduralStructures/ # Tool: Generate structures
  Cigen/               # Tool: City generation
  ProceduralCity/      # Tool: Procedural city
  TTG/                 # Tool: Terrain generation
  CityGenerator-Unity/ # Tool: City buildings
```

---

## Development Phases

### Phase 1: Environment & Map (Hien tai)
- [ ] Thiet lap terrain voi TTG / Terrain Tools
- [ ] Generate city voi ProceduralStructures / Cigen
- [ ] Xay dung map voi ProBuilder
- [ ] Thiet ke gameplay zones (safe zone, danger zone, loot areas)
- [ ] Cai dat Snaps Prototyping cho building props
- [ ] Cai dat environment packs (desert, nature)
- [ ] Setup lighting va post-processing HDRP
- [ ] Thiet ke dungeon voi Dungeon Architect

### Phase 2: Player System
- [ ] Player movement (WASD, sprint, crouch)
- [ ] Camera (first-person)
- [ ] Health system
- [ ] Interaction system
- [ ] Inventory
- [ ] Weapon system

### Phase 3: Zombie AI
- [ ] Zombie navigation (NavMesh + AI Navigation)
- [ ] Zombie behavior (wander, chase, attack)
- [ ] Zombie spawner system
- [ ] Zombie variants (fast, tank, crawler)

### Phase 4: Game Systems
- [ ] Wave system
- [ ] Loot system
- [ ] Crafting
- [ ] Survival mechanics (hunger, thirst, infection)
- [ ] Save/Load system

### Phase 5: Multiplayer (Netcode for GameObjects)
- [ ] Player sync
- [ ] Networked game state
- [ ] Server hosting
- [ ] Lobby system

### Phase 6: Polish
- [ ] Post-processing effects
- [ ] Audio design
- [ ] UI/UX
- [ ] Performance optimization

---

## How to Open Project

1. Mo Unity Hub
2. Click **Open** -> chon thu muc `e:\Project\Zombie Survival`
3. Unity se load project va tu dong resolve packages
4. Sau khi load xong, vao **Window > Package Manager** de xem tat ca packages
5. Mo scene: **Assets > Scenes** (neu chua co thi Assets > OutdoorsScene.unity)

## Map Generation Tools Usage

### 1. TTG (Terrain Generation)
- Tu menu: **Window > TTG > Terrain Generator**
- Dung de tao terrain map ban dau

### 2. ProceduralStructures
- Tu menu: **Window > Procedural Structures**
- Dung de tao building procedural (nha cua, tuong, cau thang)

### 3. Cigen
- Import tu **Assets > Cigen > Editor**
- Dung de generate city layout

### 4. Dungeon Architect
- Tu menu: **Dungeon > Dungeon Architect**
- Dung de tao dungeon layouts

### 5. ProBuilder (da cai san)
- Tu menu: **Tools > ProBuilder > ProBuilder Window**
- Dung de build map truc tiep trong Unity

---

## Git Workflow

```bash
# Clone repository
git clone https://github.com/Minhtung0510/ZombieSurvival.git

# Tao branch moi khi lam viec
git checkout -b feature/player-movement

# Commit thay doi
git add .
git commit -m "Add player movement system"

# Push branch
git push -u origin feature/player-movement

# Tao Pull Request tren GitHub
```

### Luat Commit
- `feat:` - them tinh nang moi
- `fix:` - sua loi
- `docs:` - thay doi tai lieu
- `refactor:` - tai cau truc code
- `map:` - thay doi map/terrain
- `asset:` - them asset moi

---

## Notes

- **Khong commit** thu muc `Library/`, `Logs/`, `UserSettings/` (da co trong .gitignore)
- **Khong commit** secrets/token vao repository
- **Backup** thuong xuyen: `git add . && git commit -m "checkpoint"`
