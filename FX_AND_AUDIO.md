# FX and Audio

## Overview

Aerial Thunder supplies jet, weapon, weather, mission, impact, and UI feedback systems. Most assets and tuning values are assigned in Blueprint Class Defaults, while the C++ components control runtime behavior, multiplayer ownership, cooldowns, attenuation, and cleanup.

---

## Engine Exhaust

The jet supports three exhaust visual modes:

| Mode | Use |
|---|---|
| Niagara | Niagara engine exhaust only |
| Static Mesh + Material | Material-driven static exhaust only |
| Niagara + Static Mesh + Material | Both systems together |

The root Visual Settings page can expose this choice through `JetExhaustFXComboBox`. The supplied default is `Static Mesh + Material`, which is the lighter baseline for multiplayer testing.

The static exhaust system supports:

- A primary exhaust mesh/material drive parameter.
- Idle and full-scale multipliers.
- A second long static exhaust with its own parameter and scale values.
- Boost threshold, boost drive addition, and boost scaling.
- Local and remote runtime refresh.
- Airborne spawn and respawn reinitialization.

Niagara and static exhaust are visual choices. Enabling both costs more than using one mode, so profile the combined mode before making it the project default.

---

## Weapon Audio

`UJetAudioComponent` separates owner-view and remote playback where needed.

### Gun

- Cockpit/shoulder sound
- Chase sound
- Remote exterior sound
- Separate release sound after firing stops
- Minimum fire time and release cooldown to prevent rapid press/release spam
- Remote audible-distance control

### Rockets and Missiles

- Cockpit/shoulder, chase, and remote launch sounds
- Explosion/impact sounds
- Exterior attenuation for remote players and AI

### Flares

- Local camera-view sounds
- Remote exterior sound
- Remote audible-distance control
- AI flare playback uses positional attenuation instead of global 2D playback

The hit-confirmation cue is local to the shooter. It is not broadcast to every player.

---

## Targeting and Warning Audio

Automatic and manual targeting are intentionally separate:

- Automatic targeting uses the forward lock UI and lock audio.
- Manual targeting uses the cockpit capture/TAD workflow and suppresses automatic lock UI/audio.

Warning playback includes cooldown/state protection so repeated updates do not restart the same phrase every frame. The implemented feedback covers threat and flight warnings such as missile events and altitude/pull-up conditions. Warning tuning remains Blueprint editable on the jet components.

AI and human-player missile paths both warn only the targeted victim. Standard player hard lock sends the lock warning to that victim; a successful missile launch sends the separate fired warning to the missile victim. Shooter and unrelated clients do not receive those cockpit warnings.

The project does not implement fuel-low or engine-overheat warning systems.

---

## Flyby Audio

Flyby playback is intended for high-speed passes:

- A speed threshold rejects slow nearby movement.
- Distance and pass checks determine eligibility.
- A cooldown prevents repeated playback during one pass.
- Playback is local to the listener evaluating the pass.

Tune the threshold and cooldown for the scale and speed of the map. Avoid turning flyby into a general proximity loop.

---

## Landing Gear Audio

Gear up/down uses a one-shot sound and an editable cooldown. Repeated input during the transition does not stack the gear animation and audio indefinitely. The same gear state also enables the jet's landing-assist behavior.

---

## Water and Canopy FX

The jet can trace for configured water surfaces and spawn Niagara or Cascade surface FX. Runtime cleanup prevents old particle components from remaining behind after the jet has flown away.

For Cascade emitters, particle lifetime alone does not stop a continuously looping emitter. Configure a finite emitter loop count when using a one-shot water impact.

Cockpit glass supports rain/drop feedback when interacting with configured water/cloud conditions. The effect is local presentation and does not need to be replicated as gameplay state.

---

## Thunderstorm Actor

`AAT_GM_ThunderFXActor` provides configurable thunder presentation with:

- Thunder audio
- Billboard/light flash
- Optional post-process flash
- Volume and pitch controls
- Optional distance-based sound delay
- A stable world-centered storm origin based on the actor's placed BeginPlay transform
- Eleven weighted far/right/left/high/low/front/rear placement profiles
- Signed height, distance, yaw, and random scale tuning per profile
- Weighted material variants with per-material X/Y sizing and repeat prevention

The server selects one complete event and Reliable NetMulticast sends the shared world position, material index, scale, intensity, duration, and sound delay to every client. The billboard faces each local camera, but camera/player position is not used by the default world-centered placement mode. Playback is guarded so overlapping requests do not produce doubled sound. Player-centered placement remains an optional legacy mode.

---

## Mission Radio and Music

The mission director owns sequential radio and action music:

- Each radio beat has before/after delays.
- Mission-start and waypoint-triggered sequences are supported.
- Action music has Blueprint-editable volume and fade times.
- Music can begin when a waypoint activates combat.
- Radio and music stop on mission completion, failure, or mission stop.

This is a configured cue workflow, not an automatic intensity-analysis or layered adaptive soundtrack system.

---

## Destruction and Impact FX

The supplied project includes reusable explosion, impact, weapon, water, and target-destruction presentation. Ground target destruction is server-authoritative and replicated so clients see the destroyed state as well as the FX.

Gameplay damage and destruction state should replicate. Short-lived cosmetic effects can be reconstructed locally from the replicated event when appropriate.

---

## Audio Settings

The settings subsystem supports these volume groups when the matching sound classes/mix are assigned:

- Master
- Music
- SFX
- UI
- Engine
- Weapon

The Audio Settings page also exposes a music-enabled toggle. Exact defaults are project assets/settings data and may be changed by the seller or buyer.

---

## Multiplayer Guidelines

- Use positional exterior audio for remote jets and AI.
- Keep cockpit-only sounds local to the owning player.
- Use cooldowns for warnings, thunder, flyby, gun release, and gear transitions.
- Do not replicate continuous audio every frame; replicate the gameplay state that drives it.
- Apply attenuation to AI weapon and flare cues so distant actions do not sound close.
- Profile the combined exhaust mode and dense FX scenes on both host and client.

See also:

- [Weapons and Targeting](WEAPONS_AND_TARGETING.md)
- [Mission System](MISSION_SYSTEM.md)
- [Settings Reference](SETTINGS_REFERENCE.md)
