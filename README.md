# Shadow Warrior

A browser-based 2D fighting game with combo system, particle effects, animated sprites, mobile touch controls, audio management, and local save system.

---

## Folder Structure

```
shadow-warrior/
│
├── index.html                  ← Entry point
├── style.css                   ← All styles
│
├── js/
│   ├── audio.js                ← AudioManager: music, SFX, voice announcer
│   ├── weapons.js              ← WeaponDatabase, Inventory, Shop, Loot, Rewards
│   ├── save.js                 ← SaveSystem, AutoSave, page-exit save
│   ├── AnimationManager.js     ← Sprite sheet frame sequencing
│   ├── AssetLoader.js          ← Preloads all images with progress bar
│   ├── ParticleSystem.js       ← Sparks, slashes, screen shake, screen flash
│   ├── ComboSystem.js          ← Hit streaks, multipliers, floating damage numbers
│   ├── MobileControls.js       ← Touch d-pad and action buttons
│   ├── player.js               ← Player class (movement, attacks, physics, draw)
│   ├── enemy.js                ← Enemy class (AI, attacks, physics, draw)
│   └── game.js                 ← Canvas, game loop, input, menus, victory
│
└── assets/
    ├── audio/
    │   ├── music.mp3           ← Background battle music (loop)
    │   ├── punch.mp3           ← Punch sound effect
    │   ├── kick.mp3            ← Kick sound effect
    │   ├── sword.mp3           ← Sword/weapon attack SFX
    │   └── victory.mp3         ← Victory fanfare
    │
    ├── characters/
    │   ├── shadow/             ← Shadow fighter sprite sheets
    │   │   ├── idle.png        ← 4-frame sprite sheet  (256×128 px)
    │   │   ├── walk.png        ← 6-frame sprite sheet  (384×128 px)
    │   │   ├── punch.png       ← 4-frame sprite sheet  (256×128 px)
    │   │   ├── kick.png        ← 5-frame sprite sheet  (320×128 px)
    │   │   ├── jump.png        ← 3-frame sprite sheet  (192×128 px)
    │   │   ├── hurt.png        ← 3-frame sprite sheet  (192×128 px)
    │   │   └── weapon.png      ← 5-frame sprite sheet  (320×128 px)
    │   │
    │   ├── ronin/              ← Same structure as shadow/
    │   ├── ninja/              ← Same structure as shadow/
    │   └── enemy/              ← Same structure as shadow/
    │
    ├── backgrounds/
    │   ├── dojo.png            ← Japanese dojo sunset   (1920×1080 px)
    │   ├── night.png           ← Night rooftop arena    (1920×1080 px)
    │   └── temple.png          ← Ancient temple         (1920×1080 px)
    │
    ├── weapons/
    │   ├── sword.png           ← Sword icon  (64×64 px)
    │   ├── katana.png          ← Katana icon (64×64 px)
    │   ├── staff.png           ← Staff icon  (64×64 px)
    │   ├── nunchaku.png        ← Nunchaku    (64×64 px)
    │   ├── dual.png            ← Dual blades (64×64 px)
    │   ├── shadow.png          ← Shadow Blade (64×64 px)
    │   └── dragon.png          ← Dragon Katana (64×64 px)
    │
    ├── ui/
    │   ├── health_frame.png    ← Decorative border for HP bar (420×36 px)
    │   ├── energy_frame.png    ← Decorative border for energy bar (420×24 px)
    │   └── portrait_bg.png     ← Fighter portrait background (128×128 px)
    │
    └── particles/
        ├── spark.png           ← Single spark pixel  (8×8 px)
        ├── blood.png           ← Blood splat sprite  (32×32 px)
        └── slash.png           ← Slash trail sprite  (128×32 px)
```

---

## How to Run

> **No build step required.** This is pure HTML/CSS/JS.

### Option A — Local Server (recommended)

```bash
# Python 3
cd shadow-warrior
python3 -m http.server 8080

# Then open: http://localhost:8080
```

```bash
# Node.js
npx serve shadow-warrior
```

```bash
# VS Code — install Live Server extension, right-click index.html → Open with Live Server
```

### Option B — Direct File

Opening `index.html` directly with `file://` may block audio autoplay in some browsers. Use a local server for best results.

---

## Controls

| Key | Action |
|-----|--------|
| `A` / `←` | Move Left |
| `D` / `→` | Move Right |
| `W` / `↑` / `Space` | Jump |
| `J` | Punch |
| `K` | Kick |
| `L` | Weapon Attack |
| `ESC` | Pause / Resume |
| `M` | Toggle Mute |

### Mobile Controls

Touch controls auto-activate on touch devices. A virtual d-pad appears on the left; action buttons (P / K / W) on the right. Can also be toggled manually in Settings.

---

## Characters

| Fighter | Speed | Power | Special |
|---------|-------|-------|---------|
| Shadow  | ★★★★☆ | ★★★☆☆ | Balanced |
| Ronin   | ★★☆☆☆ | ★★★★★ | +20 HP, heavy hits |
| Ninja   | ★★★★★ | ★★☆☆☆ | Higher jump, faster |

---

## Difficulty Levels

| Level | Enemy Speed | Enemy Damage | Enemy HP |
|-------|-------------|--------------|----------|
| Easy | 2 | 7 | 100 |
| Medium | 3 | 10 | 100 |
| Hard | 5 | 15 | 100 + weapon |
| Boss | 6 | 20 | 250 + weapon |

---

## Combo System

Landing consecutive hits without being hit yourself builds a combo multiplier:

- 3 hits → **COMBO!**
- 5 hits → **GREAT!** (×1.1 damage)
- 7 hits → **AMAZING!** (×1.2 damage)
- 10 hits → **INCREDIBLE!** (×1.3 damage)
- 15 hits → **UNSTOPPABLE!** (×1.5 damage)
- 20+ hits → **GODLIKE!!!** (×2.0+ damage)

Taking damage resets your combo. Peak combo and total damage are shown on the victory screen.

---

## Weapon System

### Weapon Tiers

| Weapon | Damage | Rarity | Cost |
|--------|--------|--------|------|
| Wooden Stick | 8 | Common | 50g |
| Sword | 15 | Common | 200g |
| Katana | 22 | Rare | 500g |
| Staff | 18 | Rare | 450g |
| Nunchaku | 20 | Epic | 700g |
| Dual Blades | 30 | Epic | 1200g |
| Shadow Blade | 45 | Legendary | 2500g |
| Dragon Katana | 55 | Legendary | 4000g |

Weapons can be bought via `Shop.buyWeapon(id)`, equipped via `WeaponSystem.equip(player, id)`, and drop randomly after winning via `RewardSystem.grantBattleRewards()`.

---

## Audio System

`AudioManager` handles all sound. Key methods:

```js
AudioManager.playMusic()       // Start background music
AudioManager.stopMusic()       // Stop
AudioManager.toggleMute()      // Toggle all audio (hotkey: M)
AudioManager.setMasterVolume(0.8)  // 0.0–1.0
AudioManager.setMusicVolume(0.4)
AudioManager.setEffectsVolume(0.8)
AudioManager.speak("Fight!")   // Web Speech API announcer
```

Audio files must exist at `assets/audio/`. Missing files fail silently.

---

## Save System

Games auto-save to `localStorage` every 30 seconds and on page exit.

```js
SaveSystem.save(player, enemy)   // Manual save
SaveSystem.load()                // Returns save object or null
SaveSystem.apply(player, enemy)  // Restore state from save
SaveSystem.hasSave()             // Boolean
SaveSystem.getSaveInfo()         // { lastSaved, character, health, gold }
SaveSystem.deleteSave()          // Wipe save
SaveSystem.resetProgress()       // Wipe save + reset inventory
```

Save data includes: player position, health, energy, character, weapon, enemy health/energy, inventory gold, and owned weapons.

---

## Particle System

```js
ParticleSystem.spawnHitSparks(x, y, count, color)
ParticleSystem.spawnSlash(x, y, direction)
ParticleSystem.spawnImpact(x, y)
ParticleSystem.spawnEnergyBurst(x, y, color)
ParticleSystem.shake(intensity, durationSeconds)
ParticleSystem.flash(cssColor, durationSeconds)
```

---

## Animation System

Each entity has an `anim` object created by `AnimationManager.create(character)`. Sprite sheets are horizontal strips where each frame is `frameWidth` × `frameHeight` pixels. If a sprite sheet is missing, entities fall back to geometric shapes automatically.

**State → sprite sheet file mapping:**

```
idle    → characters/{name}/idle.png    (4 frames)
walk    → characters/{name}/walk.png    (6 frames)
punch   → characters/{name}/punch.png   (4 frames)
kick    → characters/{name}/kick.png    (5 frames)
jump    → characters/{name}/jump.png    (3 frames)
hurt    → characters/{name}/hurt.png    (3 frames)
weapon  → characters/{name}/weapon.png  (5 frames)
```

---

## Required Assets (⚠ Missing — Need to Create)

Mark these as **MISSING** until you add them:

### Audio ⚠
- [ ] `assets/audio/music.mp3` — looping battle music
- [ ] `assets/audio/punch.mp3`
- [ ] `assets/audio/kick.mp3`
- [ ] `assets/audio/sword.mp3`
- [ ] `assets/audio/victory.mp3`

### Character Sprites ⚠ (sprite sheets, 64px per frame × 128px tall)
- [ ] `assets/characters/shadow/idle.png`
- [ ] `assets/characters/shadow/walk.png`
- [ ] `assets/characters/shadow/punch.png`
- [ ] `assets/characters/shadow/kick.png`
- [ ] `assets/characters/shadow/jump.png`
- [ ] `assets/characters/shadow/hurt.png`
- [ ] `assets/characters/shadow/weapon.png`
- [ ] *(same 7 files for ronin, ninja, enemy)*

### Backgrounds ⚠ (1920×1080 px PNG)
- [ ] `assets/backgrounds/dojo.png`
- [ ] `assets/backgrounds/night.png`
- [ ] `assets/backgrounds/temple.png`

### Weapon Icons ⚠ (64×64 px PNG, transparent background)
- [ ] `assets/weapons/sword.png`
- [ ] `assets/weapons/katana.png`
- [ ] `assets/weapons/staff.png`
- [ ] `assets/weapons/nunchaku.png`
- [ ] `assets/weapons/dual.png`
- [ ] `assets/weapons/shadow.png`
- [ ] `assets/weapons/dragon.png`

### UI Assets ⚠
- [ ] `assets/ui/health_frame.png`
- [ ] `assets/ui/energy_frame.png`
- [ ] `assets/ui/portrait_bg.png`

### Particle Sprites ⚠ (optional — system uses canvas drawing as fallback)
- [ ] `assets/particles/spark.png`
- [ ] `assets/particles/blood.png`
- [ ] `assets/particles/slash.png`

> All missing assets degrade gracefully. The game is fully playable with geometric fallback graphics and no audio. Add assets progressively.

---

## Future Expansion

- **Multiplayer** — WebSocket server for 1v1 online battles
- **Story Mode** — Sequential enemy encounters with cutscenes
- **Character Unlock System** — Earn characters by reaching score thresholds
- **Weapon Shop UI** — In-game screen to browse and purchase weapons
- **Animated Backgrounds** — Parallax scrolling layers
- **Special Moves** — Energy-consuming super attacks (press multiple keys)
- **Round System** — Best of 3, with round counter display
- **Leaderboard** — High score / fastest win tracking via localStorage
- **Sound Variety** — Multiple punch/kick SFX randomized per hit
- **AI Improvements** — Blocking, dodge rolling, combo patterns
- **Training Mode Expansion** — Hitbox display, frame data overlay
