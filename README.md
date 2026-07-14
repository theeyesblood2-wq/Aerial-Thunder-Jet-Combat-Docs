# Aerial Thunder: Complete Multiplayer Jet Combat Game Template

**Engine:** Unreal Engine 5.7  
**Platform:** Windows / Win64  
**Project Type:** C++ Game Template  
**Support:** See documentation and troubleshooting guides

---

## Overview

Aerial Thunder is a complete, production-ready jet combat game template for Unreal Engine 5.7. It provides a fully functional single-player and multiplayer foundation with replicated flight mechanics, weapons systems, targeting, AI dogfights, missions, UI, audio, visual effects, player progression, and optional Epic Online Services (EOS) support.

The project is designed as a ready-to-extend game framework. Developers can replace or expand aircraft, weapons, environments, missions, UI assets, and game rules while maintaining the core architecture.

### Included Content

Aerial Thunder ships as a **complete content project**, not a content-free plugin:

- Fully rigged and UE-scaled F-16 exterior aircraft with 4K materials
- Fully rigged and UE-scaled F-16 cockpit interior with 4K materials
- Functional cockpit HUD, radar, TAD (Tactical Air Display), and targeting systems
- Three playable mission maps and example environments
- Complete aircraft, cockpit, weapon, target, and UI Blueprints
- Sound effects, radio dialogue, warning systems, and music
- Materials, textures, particle systems, Niagara FX, and animations
- Single-player campaign, private LAN/editor multiplayer, and public EOS multiplayer
- Main menu, deployment, settings, loading, result, and death UI screens

**Note:** Included environments are functional examples. You are expected to create or import your own production maps, atmospheric effects, additional aircraft variants, and additional weapons systems.

---

## Quick Links

- **[Quick Start Guide](QUICK_START.md)** — Installation, first launch, and basic gameplay
- **[Input & Controls](INPUTS.md)** — Default keyboard/mouse mappings and Enhanced Input setup
- **[Architecture Overview](ARCHITECTURE.md)** — Plugin structure and core systems
- **[Flight & Cameras](FLIGHT_AND_CAMERAS.md)** — Flight modes, camera systems, and controls
- **[Weapons & Targeting](WEAPONS_AND_TARGETING.md)** — Gun, rockets, missiles, flares, and targeting
- **[HUD & Radar](HUD_AND_RADAR.md)** — Cockpit displays, HUD elements, and radar systems
- **[AI System](AI_SYSTEM.md)** — AI fighter behavior, difficulty, and dogfight tactics
- **[Mission System](MISSION_SYSTEM.md)** — Mission framework, objectives, and progression
- **[Multiplayer](MULTIPLAYER.md)** — Networking, replication, sessions, and matchmaking
- **[EOS Setup](EOS_SETUP.md)** — Epic Online Services configuration for public multiplayer
- **[UI & Settings](UI_AND_SETTINGS.md)** — Main menu, settings, player profile, and progression
- **[FX & Audio](FX_AND_AUDIO.md)** — Particle effects, audio design, and environmental effects
- **[Settings Reference](SETTINGS_REFERENCE.md)** — Configurable properties and defaults
- **[Troubleshooting](TROUBLESHOOTING.md)** — Common issues and solutions
- **[Gallery](GALLERY.md)** — Screenshots and feature overview

---

## Key Features

### Flight & Movement
- Replicated multiplayer jet flight with server authority
- Arcade flight mode for casual players
- Advanced flight mode for simulation enthusiasts
- Full 6-DoF flight control (pitch, roll, yaw, throttle)
- Automatic leveling assistance
- Landing gear and landing assistance systems
- Air brake and ground brake controls
- Engine start/shutdown sequences

### Weapons & Combat
- Gun system with tracer rounds
- Unguided rocket pods
- Guided missiles with lock-on mechanics
- Defensive flare deployment
- Automatic and manual targeting modes
- Target lock UI and audio feedback
- Server-authoritative damage and elimination

### Targeting & Awareness
- Multiplayer radar with friendly/enemy identification
- Ground target (GroundTGT) and air target (AirTGT) support
- Tactical Air Display (TAD) with target information
- Radar signature system
- Manual and automatic target cycling
- Target lock warnings and audio alerts

### Camera System
- Cockpit view (first-person)
- Shoulder camera (third-person behind aircraft)
- Chase camera (distant third-person)
- Smooth zoom and camera reset
- Configurable field of view per mode

### AI Combat
- Intelligent fighter behavior with difficulty presets
- Normal and Advanced/Ace difficulty tiers
- Gun and missile tactics
- Flare defense and countermeasures
- Obstacle avoidance and terrain awareness
- Dynamic pursuit and evasion

### Missions
- Three complete campaign missions
- Extendable mission framework for custom objectives
- Radio sequences and narrative integration
- Dynamic music and action audio
- Objective tracking and mission timers
- Mission unlock and progression saving
- Results screen with statistics

### Multiplayer
- Private LAN and local editor multiplayer
- Public internet multiplayer via Epic Online Services (EOS)
- Server-authoritative gameplay
- Replicated aircraft state and weapons
- Player profile and loadout customization
- Region and location-based matchmaking
- Spectating and respawn systems
- Killer information cards and KIA countdown
- Scoreboard and multiplayer dashboard

### UI & Settings
- Fully featured main menu
- Deployment/lobby system
- Settings menu with audio, graphics, and gameplay options
- Player profile management
- Aircraft and loadout selection
- Control scheme configuration
- Configurable UI transitions and startup logos

### Audio & FX
- Cockpit rain and water-drip effects
- Multiple exhaust modes (static mesh, Niagara, combined)
- Jet engine audio with speed-responsive sounds
- Missile launch and impact audio
- Radio communications and warnings
- Ambient weather and environmental audio
- Dynamic music system for mission intensity
- Warning system with anti-spam cooldowns

---

## Plugin Architecture

Aerial Thunder uses two independent, specialized plugins:

### AT_GM (Game Module)
Owns the game framework and global systems:
- Main menu and deployment workflows
- Player profile, settings, and progression
- Mission system, objectives, waypoints, and timers
- Health, elimination, respawn, and spectating systems
- Private and public session management
- Ground and air target systems
- Match rules, teams, scores, and result screens
- Thunder/weather actors and environmental systems

### Jet_C_MT (Jet Combat Multiplayer Template)
Owns the aircraft and flight systems:
- Flight movement and replication
- Flight control modes (arcade and advanced)
- Cockpit, shoulder, and chase cameras
- Gun, rocket, missile, and flare systems
- Automatic and manual targeting
- Radar and target signatures
- HUD and cockpit displays
- Exhaust, water, audio, and visual effects
- Landing gear and landing assistance
- AI fighter behavior and collision avoidance

**Important:** These plugins must remain independent. `AT_GM` handles the game; `Jet_C_MT` handles the aircraft. Do not merge them.

---

## Getting Started

### Installation
1. Open the Aerial Thunder project in Unreal Engine 5.7
2. Allow the editor to compile C++ modules if prompted
3. Load the main menu map or a demo level
4. Begin gameplay

### Single-Player & Private Multiplayer
No additional setup required. Open any level and press Play.

### Public Multiplayer (EOS)
Public internet multiplayer requires Epic Online Services configuration. See [EOS Setup](EOS_SETUP.md) for detailed instructions.

---

## Default Controls

| Action | Key |
|--------|-----|
| Throttle Up | Left Shift |
| Throttle Down | Left Ctrl |
| Pitch Up/Down | W / S |
| Roll Left/Right | A / D |
| Yaw Left/Right | Q / E |
| Air/Ground Brake | Space |
| Start Engine | Enter |
| Toggle Landing Gear | G |
| Auto Level | H |
| Change Camera | V |
| Reset Camera | 5 |
| Zoom Camera | Mouse Wheel |
| Fire Gun | Left Mouse Button |
| Fire Rockets | Right Mouse Button |
| Fire Missile | Middle Mouse Button |
| Deploy Flares | X |
| Auto Targeting | T |
| Next Target | 1 |
| Previous Target | 2 |
| Manual Targeting | 3 |
| Manual Target Lock | 4 |
| Warning System | K |
| Pause | Escape or P |
| Scoreboard | Tab |
| Multiplayer Dashboard | U |
| Skip Mission Intro | Space |

These are example mappings. Developers can call exposed C++/Blueprint functions from Enhanced Input or any custom input system. See [Input & Controls](INPUTS.md) for detailed wiring.

---

## System Requirements

- **Engine:** Unreal Engine 5.7
- **Platform:** Windows / Win64
- **C++ Compiler:** Visual Studio 2022 or compatible
- **RAM:** 16 GB minimum (32 GB recommended)
- **GPU:** DirectX 12 compatible, 6 GB VRAM minimum
- **Disk Space:** ~50 GB for full project with source

---

## Next Steps

1. **First Time?** → Read [Quick Start Guide](QUICK_START.md)
2. **Learning the Controls?** → Check [Input & Controls](INPUTS.md)
3. **Understanding the Codebase?** → Review [Architecture Overview](ARCHITECTURE.md)
4. **Extending the Project?** → See individual system guides
5. **Setting Up Multiplayer?** → Start with [Multiplayer](MULTIPLAYER.md), then [EOS Setup](EOS_SETUP.md) for public play

---

## Support & Documentation

Full documentation is included in this repository. Each system has its own detailed guide. If you encounter issues, see [Troubleshooting](TROUBLESHOOTING.md) or review the relevant system documentation.

---

**Aerial Thunder** — Ready to extend. Ready to deploy.
