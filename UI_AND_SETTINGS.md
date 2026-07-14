# UI & Settings Guide

## User Interface Overview

Aerial Thunder features a complete UI system with main menu, in-game HUD, settings, and post-game screens. All UI is built in Unreal Motion Graphics (UMG) for flexibility and customization.

---

## Main Menu

### Main Menu Structure

```
Aerial Thunder Main Menu
├── Single Player
│   ├── Campaign (Mission Select)
│   ├── Free Flight
│   └── Mission Replay
├── Multiplayer
│   ├── Join LAN Game
│   ├── Host LAN Game
│   └── EOS Public Match (if configured)
├── Settings
│   ├── Audio
│   ├── Graphics
│   ├── Gameplay
│   ├── Controls
│   └── Video
├── Player Profile
│   ├── Name & Account
│   ├── Loadouts
│   └── Statistics
└── Exit
```

### Single Player

#### Campaign
- **Mission Select** — Choose which mission to play
- **Difficulty** — Select Normal/Advanced/Ace
- **Aircraft** — Pick aircraft (F-16, customized variants, etc.)
- **Loadout** — Configure weapons and fuel
- **Start** — Launch mission

#### Free Flight
- **Map Select** — Choose flying area
- **Time of Day** — Dawn/Noon/Dusk/Night
- **Weather** — Clear/Cloudy/Stormy
- **Aircraft & Loadout** — Same as campaign
- **Fly Free** — No objectives, just explore

#### Mission Replay
- **Completed Missions** — Choose any previously-completed mission
- **Challenge Leaderboards** — Compete for high scores
- **New Difficulty** — Replay at harder difficulty
- **Target Score** — Attempt to beat personal best

---

## Multiplayer Menu

### Multiplayer Game Types

#### Host LAN Game
1. **Map Select** — Choose multiplayer map
2. **Game Mode** — Deathmatch/Team DM/CTF/KotH
3. **Player Limit** — Set max players (2-8)
4. **Time Limit** — Game duration
5. **Advanced Options** — Friendly fire, respawn timer, etc.
6. **Start Server** — Create game server

#### Join LAN Game
1. **Server List** — Browse available servers
2. **Or Manual IP** — Enter IP and port manually
3. **Join** — Connect to selected server

#### EOS Public Match
1. **Login** — EOS account login
2. **Mode Select** — Choose ranked/casual
3. **Game Mode** — Available modes for selection
4. **Search** — Find match (queues player)
5. **Load** — Spawn into match when ready

---

## Settings Menu

### Audio Settings

| Setting | Range | Default | Effect |
|---------|-------|---------|--------|
| **Master Volume** | 0-100% | 80% | Overall game volume |
| **Music Volume** | 0-100% | 60% | Background music level |
| **Effects Volume** | 0-100% | 80% | Sound effects level |
| **Voice Volume** | 0-100% | 70% | Radio/callouts volume |
| **Warnings Volume** | 0-100% | 90% | Warning/alert tones |
| **Reverb Enabled** | On/Off | On | Environmental audio |
| **Surround Sound** | On/Off | On | 5.1/7.1 support |

**Audio Presets:**
- **Balanced** — Equal levels across all categories
- **Immersive** — Enhanced surround; higher effects
- **Communication** — Boost voice/warnings; reduce music
- **Custom** — Adjust individually

### Graphics Settings

#### Quality Presets

| Preset | Resolution | Shadows | Effects | FPS Target |
|--------|-----------|---------|---------|-----------|
| **Low** | 1280×720 | Low | Medium | 60 FPS |
| **Medium** | 1920×1080 | Medium | High | 60 FPS |
| **High** | 2560×1440 | High | Ultra | 60 FPS |
| **Ultra** | 3840×2160 | Ultra | Ultra | 30-60 FPS |
| **Custom** | User-set | User-set | User-set | User-set |

#### Advanced Graphics Options

- **Resolution** — Screen resolution
- **Refresh Rate** — Hz (60/120/144/240)
- **V-Sync** — On/Off (reduces tearing)
- **Motion Blur** — Amount (0-100%)
- **Depth of Field** — Focus blur (0-100%)
- **Bloom** — Light bloom effect (0-100%)
- **Shadows** — Quality and distance
- **Reflections** — Water/cockpit reflections
- **Anti-Aliasing** — TAA/MSAA/FXAA
- **Ray Tracing** — On/Off (if supported)

### Gameplay Settings

| Setting | Options | Default | Effect |
|---------|---------|---------|--------|
| **Flight Mode** | Arcade/Advanced | Arcade | Flight physics |
| **Auto Level** | On/Off | On | Auto-level assist |
| **Stall Recovery** | Assisted/Manual | Assisted | Stall behavior |
| **HUD Scale** | 50-150% | 100% | HUD element size |
| **HUD Opacity** | 0-100% | 100% | HUD transparency |
| **Minimal HUD** | On/Off | Off | Immersion mode |
| **Radar Mode** | Pulse/Doppler/TWS | Pulse | Default radar |
| **Difficulty** | Normal/Advanced/Ace | Normal | AI difficulty |
| **Aim Assist** | On/Off | On | Lock-on help |
| **Friendly Fire** | On/Off | Off | Team damage |
| **Crosshair** | Predator/Circle/Custom | Predator | Reticle style |
| **Text Size** | 80-150% | 100% | UI text size |

### Controls Settings

#### Control Scheme

- **Keyboard & Mouse** — Default
- **Gamepad** — Xbox/PlayStation controller
- **Custom** — User-defined bindings

#### Sensitivity Settings

- **Mouse Sensitivity** — 0.1-2.0 (default 1.0)
- **Throttle Sensitivity** — 0.5-2.0 (default 1.0)
- **Yaw Sensitivity** — 0.5-2.0 (default 1.0)
- **Gamepad Stick Deadzone** — 0-30% (default 15%)

#### Key Bindings

All mappings customizable:
- **Flight Controls** — Pitch/Roll/Yaw/Throttle
- **Weapons** — Gun/Rockets/Missiles/Flares
- **Targeting** — Lock/Cycle/Manual
- **Camera** — Change/Reset/Zoom
- **UI** — Pause/Menu/Scoreboard

#### Inverted Controls

- **Pitch Invert** — On/Off
- **Yaw Invert** — On/Off
- **Camera Invert** — On/Off

### Video Settings

#### Display Options

- **Screen Mode** — Fullscreen/Windowed/Borderless
- **Monitor** — Select if multiple displays
- **Brightness** — 0-100%
- **Contrast** — 0-100%
- **Gamma** — Adjustment slider
- **HDR Support** — On/Off

#### Performance Options

- **Frame Rate Cap** — 30-240 FPS or Unlimited
- **Frame Rate Smoothing** — On/Off
- **Adaptive Resolution** — On/Off (adjusts resolution to maintain FPS)
- **VRR** — FreeSync/G-Sync support

---

## Player Profile

### Profile Information

#### Account Details
- **Player Name** — Callsign/Username
- **Rank** — Current player rank
- **Level** — Experience level
- **Skill Rating** — Competitive ranking
- **Join Date** — When account created
- **Total Playtime** — Hours played

#### Statistics
- **Total Kills** — Career eliminations
- **Total Deaths** — Times eliminated
- **K/D Ratio** — Kill/Death ratio
- **Win Rate** — Percentage of matches won
- **Missions Completed** — Single-player progress
- **Campaign Progress** — Highest mission reached

### Loadouts

#### Loadout Management

Each loadout saves:
- **Aircraft** — Chosen aircraft
- **Weapons** — Gun/Rocket/Missile/Flare count
- **Camouflage** — Paint scheme/cosmetics
- **Name** — Custom loadout name

#### Quick Loadouts

- **Loadout 1-5** — Five quick-select loadouts
- **Rename** — Customize loadout names
- **Copy** — Duplicate existing loadout
- **Delete** — Remove unused loadout

### Account Settings

- **Username** — Change player name (available once per month)
- **Email** — Update email address
- **Privacy** — Control visible statistics
- **Crossplay** — Enable/Disable cross-platform play
- **Notifications** — Game notifications on/off

---

## In-Game UI

### Pause Menu

When paused (Escape or P key):

```
PAUSED
├── Resume Game
├── Settings
│   ├── Audio
│   ├── Graphics
│   ├── Gameplay
│   └── Controls
├── Statistics (Mission/Match stats)
├── Objectives (Current mission objectives)
└── Exit to Menu
```

### Mission Statistics

During mission pause:
- **Elapsed Time** — Mission duration so far
- **Targets Destroyed** — Kill count
- **Accuracy** — Gun accuracy percentage
- **Fuel Remaining** — Percentage
- **Damage Taken** — Cumulative damage
- **Checkpoints** — Mission checkpoints reached

### Match Statistics

During multiplayer pause:
- **Match Time** — Duration so far
- **Your Score** — Personal score
- **Team Score** — Team total
- **K/D Ratio** — Current ratio this match
- **Objective Progress** — CTF/KotH progress

---

## Results Screen

### Mission Results

After mission completion:

```
MISSION COMPLETE
├── Score: 15,750
├── Time: 12:34
├── Accuracy: 72%
├── Bonus Unlocked: New Aircraft
├── Continue / Return to Menu
```

**Detailed breakdown:**
- Base score
- Time bonus/penalty
- Accuracy bonus
- No-damage bonus
- Completion rank (C-B-A-S)

### Match Results

After multiplayer match:

```
MATCH RESULTS - VICTORY
├── Winner: Red Team
├── Final Score: 35 - 18
├── Your Stats:
│   ├── Kills: 8
│   ├── Deaths: 2
│   ├── Objectives: 5
├── XP Gained: +500
└── Return to Menu
```

---

## HUD Customization

### HUD Options

**Edit → Project Settings → Engine → Slate → HUD**

Customize:
- HUD scale (50-200%)
- HUD opacity (0-100%)
- Font size
- Color scheme (Standard/Amber/Custom)
- Element visibility (show/hide individual elements)

### Minimal HUD

"Minimal HUD" mode removes non-critical elements:
- Removes crosshairs and reticles
- Hides score display
- Hides warnings (except critical)
- Shows only essential flight instruments
- Maximum immersion

---

## Tutorial & Help System

### Tutorial Videos

Available in settings:
- **Flight Basics** — Takeoff and landing
- **Combat** — Dogfighting and weapons
- **Multiplayer** — Online gameplay
- **Settings** — Configuration guide

### In-Game Tips

- **Loading screens** — Strategy tips
- **First mission intro** — Hands-on tutorial
- **Context help** — Available in all menus

### Help Menu

Access via **Settings → Help**:
- **Keyboard Layout** — All default controls
- **Game Terms** — Glossary of aviation/gaming terms
- **FAQ** — Common questions
- **Support** — Contact information

---

## Accessibility Options

### Visual Accessibility

- **Color Blind Mode** — Deuteranopia/Protanopia/Tritanopia support
- **Text Size** — 80-200% scaling
- **High Contrast** — Enhanced visibility mode
- **Font Selection** — Clear/Bold fonts
- **UI Scaling** — Independent from HUD scaling

### Audio Accessibility

- **Subtitles** — On/Off for all dialogue
- **Visual Warnings** — Flashing/color-coding instead of audio
- **Mono Audio** — Mono instead of stereo
- **Hearing Aid Compatible** — Special audio processing

### Motor Accessibility

- **Remappable Controls** — All keys customizable
- **Adjustable Dead Zones** — Gamepad sensitivity
- **Hold Instead of Toggle** — Options to hold keys instead of tap
- **Autorun** — Auto-cruise option for flight
- **Simplified Controls** — Reduced button count mode

---

## Customization & Cosmetics

### Aircraft Cosmetics

- **Paint Schemes** — Different liveries
- **Decals** — Custom nose art
- **Numbers** — Squadron numbers
- **Pilot Callsigns** — Radio callsign display

### Cockpit Customization

- **Interior Colors** — Cockpit color schemes
- **Instrument Styling** — HUD color variants
- **Seat Textures** — Pilot seat cosmetics

---

## Settings Tips

1. **Start with presets** — Use quality presets, then customize
2. **Match your hardware** — Set graphics appropriate for your GPU
3. **Audio balance** — Adjust warning volume higher for safety
4. **Control sensitivity** — Higher sensitivity = twitchy; lower = smooth
5. **Save custom settings** — Name your configuration for easy recall
6. **Test after changes** — Verify settings in training before mission
7. **Check accessibility** — Use color-blind mode if applicable
8. **Experiment** — Try different settings to find your preference

---

## Next Steps

- **Customize controls:** Settings → Controls
- **Adjust graphics:** Settings → Graphics
- **Create loadouts:** Player Profile → Loadouts
- **Start playing:** Single Player or Multiplayer

---

**Customize your experience. Optimize your settings. Take flight.**
