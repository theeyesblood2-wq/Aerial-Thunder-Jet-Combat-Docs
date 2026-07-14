# Architecture Overview

## Project Structure

Aerial Thunder is organized into two independent, specialized plugins:

```
Aerial Thunder Project
├── Plugins
│   ├── AT_GM (Game Module)
│   │   ├── Binaries
│   │   ├── Source
│   │   ├── Content
│   │   └── AT_GM.uplugin
│   ├── Jet_C_MT (Jet Combat Multiplayer Template)
│   │   ├── Binaries
│   │   ├── Source
│   │   ├── Content
│   │   └── Jet_C_MT.uplugin
│   └── [Other Plugins]
├── Content
│   ├── Maps
│   ├── Blueprints
│   └── Assets
├── Binaries
├── Intermediate
├── Saved
└── [Project Files]
```

---

## Plugin Responsibilities

### AT_GM (Game Module)

**Purpose:** Game framework and global systems management

#### Core Systems
- **Main Menu System** — UI, navigation, and startup workflows
- **Deployment/Lobby System** — Player team assignment, loadout selection, and match setup
- **Player Profile System** — Username validation, region, location, control preferences
- **Mission System** — Campaign progression, objectives, waypoints, timers, completion tracking
- **Elimination System** — Health, damage, death, respawn, killer information
- **Spectating System** — Spectator camera and player observation
- **Session Management** — Private LAN/editor sessions and public EOS sessions
- **Target System** — Ground targets (GroundTGT) and air targets (AirTGT)
- **Match Rules & Scoring** — Team management, score tracking, results screens
- **Environmental Systems** — Thunder/weather actors
- **Settings Management** — Game options, audio, graphics, gameplay preferences

#### Key Classes (TODO: Verify in project)
- `AGameModeBase` derivative for match rules
- `APlayerController` subclass for player input and state
- `UGameInstance` subclass for global state and EOS integration
- `UPlayerState` subclass for profile and progression data
- Various UI widgets for menus, HUD overlays, and dialogs

### Jet_C_MT (Jet Combat Multiplayer Template)

**Purpose:** Aircraft and flight system ownership

#### Core Systems
- **Flight Movement** — Flight physics, replication, and server authority
- **Flight Modes** — Arcade (simplified) and Advanced (simulation) control modes
- **Camera System** — Cockpit (FPV), shoulder (3rd-person), and chase cameras
- **Weapon Systems** — Gun, unguided rockets, guided missiles, defensive flares
- **Targeting System** — Automatic target acquisition, manual targeting, lock mechanics
- **Radar System** — 3D radar with friendly/enemy identification, target signatures
- **HUD & Cockpit** — Functional displays including TAD (Tactical Air Display), altitude, heading, speed
- **Audio System** — Engine sounds, weapons audio, radio communications, warnings
- **Visual Effects** — Exhaust (static, Niagara, combined), water interaction, impact effects
- **Landing Gear** — Deployment, audio, landing assistance
- **AI Fighter** — Intelligent dogfighting behavior with difficulty presets
- **Collision Avoidance** — Terrain and obstacle awareness

#### Key Classes (TODO: Verify in project)
- `APawn` derivative for the playable aircraft
- `UCharacterMovementComponent` or custom `UPawnMovementComponent` for flight physics
- `UActorComponent` subclasses for weapons, radar, and targeting
- `AAIController` subclass for AI fighter behavior
- Various Blueprint actors for missiles, flares, and effects

---

## Communication Between Plugins

The two plugins maintain clear separation of concerns:

### AT_GM → Jet_C_MT
- Spawn and possess aircraft for players
- Pass player profile (username, loadout, difficulty) to aircraft
- Request aircraft state for HUD display
- Listen for aircraft elimination events

### Jet_C_MT → AT_GM
- Report weapon impacts and target elimination
- Signal player death/KIA events
- Broadcast radar data for scoreboard/minimap
- Send audio/HUD feedback to game systems

### Shared Data
- Player state (name, team, score)
- Match state (active players, objectives, timer)
- Target information (friendly/enemy, location, status)

---

## Networking Architecture

### Replication Model
- **Server-Authoritative:** All game-critical decisions (damage, elimination, scoring) are made on the server
- **Client-Predicted:** Aircraft position, rotation, and inputs are predicted on clients for smooth visuals
- **Replicated Variables:** Flight state, weapon state, health, team assignment
- **RPC Calls:** Used for one-time events (weapon fire, target lock, radio callouts)

### Session Types

#### Private Sessions (Local/LAN)
- Listen server architecture (one player hosts, others join)
- No internet required
- Full replicated gameplay
- Suitable for testing and local multiplayer

#### Public Sessions (EOS)
- Dedicated server or peer-to-peer with session management
- Requires Epic Online Services configuration
- Matchmaking and region-based player discovery
- Player profile and progression persistence

---

## Data Flow

### Player Input → Aircraft Control
```
Player Input (Keyboard/Mouse)
  ↓
PlayerController (AT_GM)
  ↓
Aircraft Pawn (Jet_C_MT)
  ↓
Flight Movement Component
  ↓
Network Replication (Server Authority)
  ↓
All Clients Updated
```

### Weapon Fire → Target Elimination
```
Fire Input (Left/Right/Middle Mouse)
  ↓
Weapon Component (Jet_C_MT)
  ↓
Server RPC: Fire_Implementation()
  ↓
Target Detection (Trace/Sphere Check)
  ↓
Damage Application
  ↓
Elimination Event → AT_GM
  ↓
Score Update, Killer Info Card, RIP Screen
```

### Mission System Flow
```
Mission Start (AT_GM)
  ↓
Objectives Broadcast to Player HUD (Jet_C_MT)
  ↓
Player Completes Objective
  ↓
Event Reported → AT_GM
  ↓
Objective Marked Complete
  ↓
Mission Timer / Results Screen
```

---

## Blueprint vs. C++

### Core Systems (C++)
These are implemented in C++ for performance and server authority:
- Flight physics and replication
- Weapon damage calculation
- Networking and session management
- AI behavior and pathfinding

### Extensible Systems (Blueprint)
These are implemented (or can be extended) in Blueprint for flexibility:
- Aircraft variants and customization
- Weapon configurations
- UI screens and menus
- Mission objectives and scripting
- Environmental effects

---

## Configuration & Customization

### Per-Aircraft Customization
Replace or extend aircraft blueprints in `Jet_C_MT / Content / Aircraft/`.

### Weapon Systems
Create new weapon blueprints derived from base weapon classes in `Jet_C_MT / Content / Weapons/`.

### Mission Framework
Extend mission system in `AT_GM / Source / Mission/` or create new mission blueprints.

### UI Customization
Modify UI widgets in `AT_GM / Content / UI/` and `Jet_C_MT / Content / UI/`.

### Settings
Game configuration stored in project settings and player profile. See [Settings Reference](SETTINGS_REFERENCE.md).

---

## Performance Considerations

### Network Bandwidth
- Flight state replication optimized with quantization and delta compression
- Radar data sent at lower frequency (typically 2-5 Hz)
- Weapon fire uses RPC for instant, reliable transmission

### Server Load
- Physics simulation runs on server for authoritative flight
- Target detection and damage calculation performed server-side
- AI fighters simulate on server (dedicated server) or listen server

### Client Performance
- Client-side prediction smooths aircraft movement
- Audio and particle effects are local (not replicated)
- HUD rendering is client-only

---

## Extensibility Points

### Adding New Aircraft
1. Create a new Blueprint child of the base aircraft pawn in `Jet_C_MT`
2. Configure mesh, materials, and cockpit interior
3. Tune flight parameters (mass, drag, thrust)
4. Register in aircraft selection menu

### Adding New Weapons
1. Create Blueprint or C++ class derived from weapon base
2. Define projectile/effect behavior
3. Wire into fire input events
4. Add to loadout customization

### Adding New Missions
1. Create mission blueprint in `AT_GM`
2. Define objectives and waypoints
3. Script mission events and audio
4. Register in mission selection menu
5. Integrate into progression system

### Adding New Maps
1. Create a new level in `Content / Maps/`
2. Place spawn points for players
3. Add ground and air targets if applicable
4. Configure match rules in GameMode
5. Register in map rotation

---

## Plugin Dependencies

### Jet_C_MT Dependencies
- Enhanced Input System (for input handling)
- Niagara (for particle effects)
- Paper2D (if using 2D radar elements)
- Audio Engine (built-in)

### AT_GM Dependencies
- Online Subsystem (for session management)
- Online Subsystem EOS (optional, for public multiplayer)
- Niagara (for environmental effects)

---

## Key Takeaways

1. **Two Independent Plugins:** AT_GM handles the game; Jet_C_MT handles the aircraft. Keep them decoupled.
2. **Server Authority:** All game-critical decisions happen on the server for fair multiplayer.
3. **Clear Communication:** Use events and delegates to communicate between systems.
4. **Replication First:** Network replication is built into core systems from the start.
5. **Extensible Design:** Replace or extend aircraft, weapons, missions, and UI without modifying core code.

---

For more details, see system-specific guides:
- [Flight & Cameras](FLIGHT_AND_CAMERAS.md)
- [Weapons & Targeting](WEAPONS_AND_TARGETING.md)
- [Mission System](MISSION_SYSTEM.md)
- [Multiplayer](MULTIPLAYER.md)
