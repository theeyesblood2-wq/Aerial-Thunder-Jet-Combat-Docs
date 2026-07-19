# Aerial Thunder: Complete Multiplayer Jet Combat Game Template

**Engine:** Unreal Engine 5.7  
**Platform:** Windows / Win64  
**Project Type:** C++ game template with Blueprint-configurable systems  
**Developer:** JB - AT: Games

---

## Overview

Aerial Thunder is a complete, extendable jet combat game template for Unreal Engine 5.7. It combines replicated jet flight, weapons, targeting, AI dogfights, missions, multiplayer sessions, user interfaces, settings, audio, and visual effects in one playable C++ project.

The project is intended as a foundation for developers building their own jet game. Aircraft, weapons, maps, missions, UI, audio, effects, and game rules can be replaced or extended without merging the two core plugins.

### Included Content

Aerial Thunder ships as a complete example project:

- Rigged, UE-scaled F-16 exterior aircraft with high-resolution materials
- Rigged, UE-scaled F-16 cockpit interior with high-resolution materials
- Cockpit HUD, radar display, TAD capture display, and targeting systems
- Free-flight, mission, and online example maps
- Aircraft, weapon, target, mission, menu, settings, and deployment Blueprints
- Sound effects, radio dialogue, warning audio, action music, and UI audio
- Materials, textures, Niagara and Cascade effects, animations, and UI assets
- Single-player, mission, local multiplayer test, private session, and public EOS workflows
- Main menu, loading, deployment, pause, result, killed-in-action, and settings screens

The included environments are functional examples. Production releases will normally add custom maps, atmosphere, aircraft variants, weapons, effects, and UI art.

---

## Quick Links

- **[Quick Start Guide](QUICK_START.md)** - Installation, first launch, and first flight
- **[Input and Controls](INPUTS.md)** - Runtime rebinding and keyboard, mouse, Xbox-compatible defaults
- **[Architecture Overview](ARCHITECTURE.md)** - Plugin ownership and core systems
- **[Flight and Cameras](FLIGHT_AND_CAMERAS.md)** - Flight presets, cameras, and landing support
- **[Weapons and Targeting](WEAPONS_AND_TARGETING.md)** - Gun, rockets, missiles, flares, and targeting
- **[HUD and Radar](HUD_AND_RADAR.md)** - Cockpit displays, radar contacts, and target information
- **[AI System](AI_SYSTEM.md)** - AI fighter behavior, difficulty, weapons, and avoidance
- **[Mission System](MISSION_SYSTEM.md)** - Mission directors, waypoints, audio beats, targets, and progression
- **[Multiplayer](MULTIPLAYER.md)** - Replication, sessions, teams, respawn, and spectating
- **[EOS Setup](EOS_SETUP.md)** - Optional Epic Online Services configuration
- **[UI and Settings](UI_AND_SETTINGS.md)** - Menus, profile, settings, and deployment
- **[FX and Audio](FX_AND_AUDIO.md)** - Exhaust, weather, weapon audio, and feedback
- **[Settings Reference](SETTINGS_REFERENCE.md)** - Important Blueprint-editable properties
- **[Troubleshooting](TROUBLESHOOTING.md)** - Common setup and runtime issues
- **[Gallery](GALLERY.md)** - Project screenshots and feature examples

---

## Key Features

### Flight and Movement

- Replicated high-speed jet movement
- Server authority with client prediction, reconciliation, and visual smoothing
- Arcade and Advanced control presets
- Pitch, roll, yaw, throttle, braking, and auto-level controls
- Airborne and grounded start support
- Landing gear cooldown, gear audio, and configurable landing assistance
- Ground movement, takeoff, landing, water interaction, crash, and respawn support

### Weapons and Combat

- Replicated machine gun with tracer projectiles and release audio
- Unguided rockets
- Lock-on missiles
- Defensive flares
- Automatic and manual targeting modes
- Configurable ammo and pylon visibility
- Server-authoritative damage, elimination, and suicide feedback

### Targeting and Awareness

- Radar contacts for multiplayer jets, AirTGT actors, and GroundTGT actors
- Friendly and enemy color identification
- Automatic forward targeting with lock UI and audio
- Manual cockpit targeting using a dedicated capture display
- Target lock and missile warning feedback
- Radar signature and marker components

### Camera System

- Cockpit camera
- Shoulder camera
- Chase camera
- Camera zoom and reset
- Local camera handling separated from replicated movement
- Configurable killed-in-action spectator camera behavior

### AI Combat

- Normal and Advanced menu difficulty choices
- Internal Blueprint-editable AI difficulty presets and weapon damage values
- Gun and missile attacks
- Flare defense and threat reaction
- Pursuit, attack passes, break-away behavior, and six-pressure behavior
- Terrain and obstacle sensor avoidance

### Missions

- Mission 01 flight and waypoint training
- Mission 02 takeoff and landing training
- Mission 03 combat mission with radio, targets, AI, timer, and action music
- Reusable MissionDirector, MissionIntroDirector, and waypoint framework
- Blueprint-editable radio beat sequencing and delays
- Required target tracking, mission completion, failure, result, and progression saving
- Mission unlocks and next-mission travel

### Multiplayer

- Local multi-player PIE testing
- Private session workflow
- Optional public internet sessions through EOS
- Replicated aircraft, weapons, damage, targets, teams, and match state
- TDM scoreboard and multiplayer dashboard
- Killed-in-action countdown, killer information card, respawn, and spectating
- Player profile, loadout, control mode, region, and location information

### UI and Settings

- Main menu and deployment workflows
- Aircraft, loadout, map, control, and AI selection
- Graphics, audio, visual, controls, UI, and profile settings
- Saved username, region, location, and EOS login state
- Configurable screen transitions and startup logo animation
- Selectable jet exhaust visual mode
- Runtime keyboard, mouse, gamepad button, trigger, and analog-stick rebinding
- Primary/Secondary slots, local save, full reset, and right-click single-slot reset

### Audio and FX

- Static-mesh, Niagara, and combined engine exhaust modes
- Long static exhaust support
- Engine, afterburner, weapon, flare, warning, flyby, and gear audio
- Distance-limited remote weapon and flare audio
- Mission radio and action music sequencing
- Shared world-centered Thunder actor with weighted placement profiles, material variants, and overlap protection
- Water-surface effects and cockpit rain/drip feedback
- Warning cooldowns that prevent repeated audio spam

---

## Plugin Architecture

Aerial Thunder uses two independent runtime plugins.

### AT_GM

`AT_GM` owns the game framework:

- Main menu, settings, profile, and deployment workflows
- Missions, objectives, waypoints, progression, results, and loading
- Health, elimination, respawn, spectating, and killer information
- Session creation, discovery, joining, teams, scoring, and match state
- Ground and air target actors
- Thunder and global game-side systems

### Jet_C_MT

`Jet_C_MT` owns the aircraft:

- Jet movement, prediction, replication, and visual smoothing
- Control presets and cameras
- Gun, rocket, missile, and flare systems
- Automatic and manual targeting
- Radar contacts and signatures
- Cockpit HUD integration
- Exhaust, water, audio, and feedback systems
- Landing gear and landing assistance
- AI fighter behavior and avoidance

> **Architecture rule:** `AT_GM` and `Jet_C_MT` remain separate. Each plugin performs its own job and communicates through exposed runtime data and APIs.

---

## Getting Started

### Open the Project

1. Install Unreal Engine 5.7 and Visual Studio 2022 with Unreal Engine C++ tools.
2. Open `AT_JetMP.uproject`.
3. Allow Unreal Engine to compile project modules when requested.
4. Load `/Game/AT_Games/AT_GM_Base/Maps/Map_MainMenu`.
5. Press Play.

### Offline and Local Testing

Single-player, missions, free flight, and local multiplayer testing work without EOS product credentials.

### Public Multiplayer

Public internet multiplayer requires your own Epic Online Services product, sandbox, deployment, client, and artifact values. The distributed template must not contain the seller's private EOS credentials. Follow [EOS Setup](EOS_SETUP.md).

---

## Default Controls

| Action | Default input |
|---|---|
| Throttle up / down | Left Shift / Left Ctrl |
| Pitch | W / S |
| Roll | A / D |
| Yaw | Q / E |
| Air or ground brake | Space |
| Start engine | Enter |
| Toggle landing gear | G |
| Auto level | H |
| Change camera | V |
| Reset camera | 5 |
| Zoom camera | Mouse wheel |
| Fire gun | Left Mouse Button |
| Fire rockets | Right Mouse Button |
| Fire missile | Middle Mouse Button |
| Deploy flares | X |
| Toggle automatic targeting | T |
| Next / previous target | 1 / 2 |
| Toggle manual targeting | 3 |
| Manual target lock | 4 |
| Toggle warning system | K |
| Pause | Escape or P |
| TDM scoreboard | Tab |
| Multiplayer dashboard | U |
| Skip mission intro | Space, while an intro is active |

These mappings are defined in the example project's input configuration. The C++ systems also expose callable functions for custom Blueprint or Enhanced Input wiring.

Players can change these mappings from **Settings > Key Bindings**, including keyboard, mouse, and supported gamepad inputs. See [Inputs](INPUTS.md) for the packaged Xbox-compatible layout, save/reset behavior, and device notes.

---

## Requirements

- Unreal Engine 5.7
- Windows 64-bit
- Visual Studio 2022 with Desktop development with C++ and Unreal Engine tooling
- DirectX 12 compatible hardware suitable for Unreal Engine 5 projects

---

## Next Steps

1. Read the [Quick Start Guide](QUICK_START.md).
2. Review [Input and Controls](INPUTS.md).
3. Learn the ownership boundary in [Architecture Overview](ARCHITECTURE.md).
4. Configure public multiplayer only after reading [EOS Setup](EOS_SETUP.md).
5. Use the individual system guides when extending the project.

---

**Aerial Thunder** - a playable jet combat foundation built to be extended.
