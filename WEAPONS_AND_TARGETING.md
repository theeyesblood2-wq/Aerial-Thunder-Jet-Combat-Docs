# Weapons and Targeting Guide

## Overview

The supplied jet supports four combat actions:

- machine gun,
- air-to-ground rockets,
- guided missiles,
- defensive flares.

Weapon state, ammo, projectile spawning, damage, visual pylons, audio, and multiplayer replication are handled by the `Jet_C_MT` plugin. Mission scoring, elimination feedback, teams, and respawn belong to `AT_GM`.

## Default Weapon Controls

| Action | Default input |
|---|---|
| Fire gun | Left Mouse Button |
| Fire rockets | Right Mouse Button |
| Fire missile | Middle Mouse Button |
| Deploy flares | X |
| Toggle auto targeting | T |
| Cycle next target | 1 |
| Cycle previous target | 2 |
| Manual target focus | 3 |
| Manual lock on/off | 4 |

## Machine Gun

The gun is intended for close and medium combat passes. Its ammo, damage, rate, projectile behavior, muzzle setup, audio, and FX are configurable on the jet.

The project includes:

- local cockpit/shoulder gun audio,
- chase camera gun audio,
- spatialized remote gun audio,
- a gun-release sound after a valid firing burst,
- cooldown protection against release-sound spam,
- replicated firing for multiplayer observers.

The gun projectile spawn path has been adjusted for high-speed multiplayer flight so the owning client does not see bullets appearing behind the aircraft.

## Rockets

Rockets are unguided air-to-ground weapons. Their class, ammo, damage, launch sockets, audio, FX, and replication are configurable.

Use a stable attack line and allow enough distance to recover from the pass. Rockets do not use the guided missile lock workflow.

## Guided Missiles

Missiles require a valid target lock. The targeting component supplies the locked actor to the weapon component, which then launches the configured missile projectile.

The project supports:

- target acquisition and cycling,
- lock timing and lock confirmation,
- target loss handling,
- air and ground target support where configured,
- missile warning audio,
- defensive flare interaction,
- replicated launch and projectile behavior.

Exact range, cone, lock time, ammo, damage, and guidance values are Blueprint-editable. Treat the supplied values as a starting point, not a fixed specification.

## Flares

Flares are defensive countermeasures used against incoming guided missiles. Flare ammo, cooldown, projectile/actor class, FX, and audio are configurable.

Remote flare audio is distance-gated and spatialized. This prevents an AI or remote player from sounding close when deploying flares far from the listener.

Flares improve survival but do not guarantee that every missile will miss. Effectiveness depends on projectile and countermeasure tuning.

## Loadout Presets

The sample jet supplies these loadouts:

| Loadout | Gun | Missiles | Rockets |
|---|---:|---:|---:|
| Full | Yes | Yes | Yes |
| AA + Gun | Yes | Yes | No |
| AG + Gun | Yes | No | Yes |
| Gun Only | Yes | No | No |
| Empty | No | No | No |

Flares and exact ammo values remain controlled by the preset configuration.

The active loadout is stored on the jet and can be selected by the main menu or deployment flow before spawn.

### Pylon Visuals

Missile and rocket pylon meshes update with the current loadout and ammo. When the relevant ammo reaches zero, the corresponding weapon visuals are hidden instead of remaining on the aircraft.

## Two Targeting Modes

Aerial Thunder separates automatic targeting from manual cockpit targeting.

### Automatic Targeting

Automatic targeting uses the forward-facing gameplay targeting system.

It provides:

- target acquisition,
- next/previous target cycling,
- lock widget presentation,
- lock and confirmation audio,
- missile firing against the current valid lock.

### Manual Targeting

Manual targeting uses the cockpit Tactical Air Display workflow and a dedicated scene capture.

It provides:

- TAD camera activation,
- manual focus selection,
- manual lock toggle,
- configurable capture performance, FOV, filtering, and aim behavior.

Manual mode intentionally does not use the automatic lock widget or automatic targeting audio. Switching to manual mode suppresses the automatic UI and stops its lock audio so the two modes remain cleanly separated.

## Supported Targets

Targeting and radar can work with:

- `AirTGT` actors,
- `GroundTGT` actors,
- AI jets,
- multiplayer player jets,
- additional configured target classes and tags.

Target classes must be configured consistently across the targeting, radar, health, and team systems.

## Multiplayer Rules

Weapon authority remains on the server while local presentation is optimized for responsiveness.

Key rules:

- Damage and confirmed eliminations are server-authoritative.
- Local-only cockpit sounds are not broadcast to every player.
- Remote weapon sounds use distance and attenuation rules.
- Projectiles and weapon state replicate to other players.
- Killer information is passed to the killed-in-action and spectating workflow.
- Human hard-lock warning is delivered only to the targeted player's owning client.
- A successful human missile launch sends the separate fired warning only to that missile victim.
- AI and human warning paths remain separated to prevent duplicate warnings.

Poor internet conditions can still make remote rockets, missiles, or flares appear slightly delayed. Validate changes in both local multiplayer and real EOS sessions.

## Blueprint Configuration Areas

Common configuration groups include:

- weapon enable flags,
- ammo and infinite-ammo flags,
- projectile classes,
- launch sockets,
- damage and explosion values,
- gun fire and release audio,
- rocket, missile, and flare audio,
- remote audible distances and attenuation,
- targeting trace, cone, timing, and filtering,
- manual targeting capture and lock settings,
- loadout presets and pylon visuals.

## Troubleshooting

### A missile will not fire

- Confirm the selected loadout includes missiles.
- Confirm missile ammo is greater than zero.
- Acquire a valid lock first.
- Check the target class or tag filters.
- Verify automatic and manual modes are not both trying to control the lock.

### Rockets or missiles appear behind a fast jet

- Test the packaged build as both host and joined client.
- Confirm the latest owner-side high-speed spawn correction is present.
- Check latency before modifying launch sockets.
- Do not add a second Blueprint projectile spawn path.

### Remote gun or flare audio is audible from too far away

- Assign the intended exterior action attenuation asset.
- Check the remote audible distance on the jet audio component.
- Verify the sound is spawned at the aircraft location, not as 2D audio.

### Weapon meshes remain after ammo reaches zero

- Confirm pylon visual updates are enabled.
- Check that ammo changes pass through the weapon component.
- Verify the configured pylon components are the meshes actually used by the derived jet Blueprint.

### Manual targeting still plays auto-lock audio

- Enable suppression of automatic targeting audio during manual lock.
- Confirm the manual mode switch calls the supplied targeting mode path.
- Remove duplicate Blueprint audio calls.

## Related Guides

- [INPUTS.md](INPUTS.md)
- [HUD_AND_RADAR.md](HUD_AND_RADAR.md)
- [AI_SYSTEM.md](AI_SYSTEM.md)
- [MULTIPLAYER.md](MULTIPLAYER.md)
- [FX_AND_AUDIO.md](FX_AND_AUDIO.md)
