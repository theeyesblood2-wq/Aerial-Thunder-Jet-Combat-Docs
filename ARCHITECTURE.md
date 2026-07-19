# Architecture Overview

## Core Rule

Aerial Thunder is built around two separate runtime plugins:

```text
AT_GM <-> Jet_C_MT
```

They cooperate through gameplay state, components, events, and configured classes, but each plugin owns its own job. Keep that separation when extending the project.

---

## Plugin Layout

```text
AT_JetMP
|-- Config
|-- Content
|-- Plugins
|   |-- AT_GM
|   |   |-- Content
|   |   |-- Source/AT_GM
|   |   `-- AT_GM.uplugin
|   `-- Jet_C_MT
|       |-- Source/Jet_C_MT
|       `-- Jet_C_MT.uplugin
`-- AT_JetMP.uproject
```

Both plugins are Win64 runtime plugins for Unreal Engine 5.7. `AT_GM` can contain content. `Jet_C_MT` is the C++ flight/combat module and does not declare plugin content.

---

## AT_GM Responsibilities

`AT_GM` owns the game framework around the jet:

- root menu, settings, profile, and screen transitions
- free-flight, mission, and multiplayer travel setup
- mission directors, intro directors, waypoints, progress saves, and result screens
- private and public session menus and session subsystem
- player state, game state, game modes, team scoring, and match results
- health, elimination, KIA countdown, killer information, respawn, and spectating
- AirTGT and GroundTGT actors
- loading, pause, briefing, scoreboard, and match widgets
- thunder, global post-process, and other game-level presentation actors
- local-player runtime input binding, validation, persistence, and settings integration

Representative classes include:

| Area | Classes |
|------|---------|
| Game rules | `AAT_GM_BaseGameMode`, `AAT_GM_SessionGameMode`, `AAT_GM_GameState` |
| Player state | `AAT_GM_PlayerController`, `AAT_GM_SessionPlayerController`, `AAT_GM_PlayerState` |
| Sessions | `UAT_GM_SessionSubsystem`, `UAT_GM_SessionMenuWidget`, `UAT_GM_SessionRowWidget` |
| Missions | `AAT_GM_MissionDirectorActor`, `AAT_GM_MissionIntroDirector`, `AAT_GM_MissionWaypointActor` |
| Targets | `AAT_GM_AirTGT`, `AAT_GM_GroundTGT`, `UAT_GM_MarkerComponent` |
| UI/settings | `UAT_GM_MainMenuWidget`, `UAT_GM_SettingsPanelWidget`, `UAT_GM_UserSettingsSubsystem` |
| Elimination | `UAT_GM_HealthComponent`, `UAT_GM_KilledInActionWidget`, `UAT_GM_MissionResultWidget` |

---

## Jet_C_MT Responsibilities

`Jet_C_MT` owns the aircraft itself:

- playable replicated jet pawn
- airborne and ground movement
- cockpit, shoulder, and chase cameras
- gun, rockets, missiles, flares, tracers, and pylon visuals
- automatic and manual targeting
- radar signatures, tactical radar, and radar widget data
- cockpit HUD and animation instance values
- engine, weapon, warning, flyby, and release audio behavior
- exhaust, long exhaust, water interaction, and jet-local FX
- AI pilot combat behavior and avoidance

Representative classes include:

| Area | Classes |
|------|---------|
| Aircraft | `AJetPawn`, `UJetMovementComponent`, `UJetGroundMovementComponent` |
| Weapons | `UJetWeaponComponent`, `AJetMissile`, `AJetFlare`, `AJetTracer`, `UJetPylonVisualsComponent` |
| Targeting/radar | `UJetTargetingComponent`, `UJetManualTargetingComponent`, `UJetTacticalRadarComponent`, `UJetRadarSignatureComponent` |
| HUD/animation | `AJetCockpitHUD`, `UJetCockpitHUDWidget`, `UJetRadarWidget`, `UJetAnimInstance` |
| Audio/FX | `UJetAudioComponent`, `UJetFXComponent` |
| AI | `UJetAIPilotComponent` |

---

## Ownership Boundary

Use this rule when deciding where a new feature belongs:

| Feature | Owner |
|---------|-------|
| Jet movement or camera feel | `Jet_C_MT` |
| Weapon firing or jet-local FX/audio | `Jet_C_MT` |
| Radar and targeting behavior | `Jet_C_MT` |
| Mission flow or result screen | `AT_GM` |
| Lobby, EOS session, teams, or scoring | `AT_GM` |
| Profile, settings save, or root menu | `AT_GM` |
| Air/ground mission target framework | `AT_GM` |

Do not copy jet systems into `AT_GM`, and do not move menu/session/mission authority into `Jet_C_MT`.

---

## Runtime Flow

### Offline and Mission Launch

```text
Root menu selection
  -> AT_GM stores aircraft/loadout/control/AI choices
  -> level travel
  -> game mode or mission intro director spawns the configured jet
  -> player controller possesses the jet
  -> Jet_C_MT runs flight, camera, targeting, weapons, audio, and FX
```

Mission 01 and Mission 02 may use an intro sequence before spawn/possession. Mission 03 supports a no-sequence start with fade, radio beats, waypoint activation, combat targets, AI, action music, timer, and results.

### Elimination and Respawn

```text
Weapon or collision damage
  -> server-authoritative health/elimination handling
  -> AT_GM records the elimination and killer information
  -> KIA widget and countdown
  -> optional killer/world spectating view
  -> respawn and possess a new jet
```

The killer card can display player or AI information. Player profile fields are replicated through the multiplayer game framework; AI difficulty comes from the configured AI preset.

### Multiplayer Session

```text
Session menu
  -> UAT_GM_SessionSubsystem creates or finds a session
  -> host travels as a listen server
  -> joined players travel to the advertised session
  -> AT_GM owns teams, scoring, respawn, and match state
  -> Jet_C_MT owns each replicated aircraft
```

Public sessions require a valid EOS setup and login. Offline modes remain available when EOS is disabled. Private/editor testing can use the project's non-EOS session path.

---

## Networking Model

The game uses server authority for match-critical state such as damage, elimination, scoring, spawning, and session state. Jet movement and combat systems include replicated state and remote presentation handling for multiplayer flight.

Important design points:

- the host is the listen server in the supplied workflow
- public EOS play is session-based peer hosting, not a supplied dedicated-server service
- local visual/audio effects are driven on each machine from replicated gameplay events and state
- weapon spawning has dedicated handling to keep high-speed muzzle and pylon origins visually aligned
- remote jet movement uses smoothing and reconciliation logic tuned for the high-speed aircraft
- network quality can still affect a joined client's input response and remote aircraft presentation

Do not describe the template as cheat-proof or promise zero-latency behavior. Always validate changes as standalone, host, and joined client.

---

## C++ and Blueprint Roles

The project is a C++ foundation with Blueprint configuration and presentation on top.

### C++

- replicated game and aircraft logic
- movement, weapons, targeting, radar, AI, health, sessions, and mission framework
- reusable actor components and base widgets
- Blueprint-callable and Blueprint-editable integration points

### Blueprint and Content

- concrete jet and AI jet Blueprint classes
- meshes, animation Blueprint, cockpit, HUD widgets, and visual layout
- per-actor tuning, sound cues, materials, Niagara systems, and maps
- mission director instances, waypoint instances, target lists, radio beats, and result presentation
- menu screen hierarchy and project-specific selections

Prefer editing exposed defaults and child Blueprints before changing shared C++ behavior.

---

## Extending the Project

### Add an Aircraft

1. Create a child of the supplied jet pawn Blueprint/class.
2. Assign the skeletal mesh, animation class, sockets, cockpit, and cameras.
3. Configure movement, audio, FX, targeting, radar signature, weapons, and pylon visuals.
4. Add the aircraft to the appropriate root-menu selection entry.
5. Test offline, respawn, host, and joined-client behavior.

### Add a Weapon or Loadout

1. Configure or extend the relevant `Jet_C_MT` weapon/projectile class.
2. Set projectile class, sockets, ammo, damage, audio, and FX.
3. Add the loadout to the root/deployment selections.
4. Verify ammo depletion and pylon visibility.
5. Test remote spawning at high speed.

### Add a Mission

1. Create a map and place the required player/AI start actors.
2. Add configured mission director and optional intro director actors.
3. Add ordered/tagged waypoint actors and target actors.
4. Configure mission ID, progression, timer, audio beats, activation, results, and next mission.
5. Register the mission in the root menu and test locked/unlocked progression.

Mission 03 is the best reference for an extensible combat mission.

### Add a Map

1. Create the level and set its game mode/world settings.
2. Add the required spawn actors and gameplay actors.
3. Register the map in the root or session menu data.
4. Add the map to packaging/cook settings.
5. Test direct editor launch and travel from the menu.

---

## Plugin Dependencies

### AT_GM

- Online Subsystem
- Online Subsystem Utils
- Online Subsystem Null
- Niagara
- optional project-level Online Subsystem EOS configuration for public internet play

### Jet_C_MT

- Niagara

The project input configuration uses Unreal's Enhanced Player Input and Enhanced Input Component classes, while gameplay is exposed through named mappings in `DefaultInput.ini`.

---

## Related Guides

- [Flight and Cameras](FLIGHT_AND_CAMERAS.md)
- [Weapons and Targeting](WEAPONS_AND_TARGETING.md)
- [Mission System](MISSION_SYSTEM.md)
- [Multiplayer](MULTIPLAYER.md)
- [EOS Setup](EOS_SETUP.md)
