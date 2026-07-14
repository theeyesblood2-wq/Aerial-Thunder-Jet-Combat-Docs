# Weapons and Targeting

This guide covers the included gun, rockets, missiles, flares, loadouts, pylons, automatic targeting, and manual targeting workflow.

## Core Components

The combat stack belongs to `Jet_C_MT`:

- `UJetWeaponComponent` owns weapon state, ammo, firing, damage, projectile/trace behavior, and weapon audio/FX requests.
- `UJetTargetingComponent` owns automatic forward targeting and lock state.
- `UJetManualTargetingComponent` owns the manual TAD/capture targeting workflow.
- `UJetPylonVisualsComponent` shows and hides mounted weapon meshes from the active loadout and remaining ammo.
- `AJetMissile`, `AJetFlare`, and `AJetTracer` provide runtime weapon actors/effects.

Damage and elimination are resolved through the replicated gameplay layer. Do not add duplicate client-side damage in a Blueprint.

## Included Weapons

| System | Description |
|---|---|
| Gun | Rapid-fire cannon with tracer, heat/state, range, damage, and release audio support. |
| Rockets | Unguided air-to-ground projectiles with configurable launch and impact behavior. |
| Missiles | Guided projectiles requiring a valid target lock. |
| Flares | Defensive countermeasures used by players and AI. |

### Default Inputs

| Action | Default input |
|---|---|
| Fire gun | Left Mouse Button |
| Fire rockets | Right Mouse Button |
| Fire missile | Middle Mouse Button |
| Deploy flares | X |

## Loadout Presets

The included runtime loadout names are:

- `Full`
- `AA_Gun`
- `AG_Gun`
- `GunOnly`
- `Empty`

Each `FJetLoadoutRuntimePreset` can enable or disable gun, AA missiles, AG rockets, and flares, then assign the starting ammunition for each system.

Use `ApplyRuntimeLoadoutByName` or `ApplyJetLoadoutPresetByName` when applying a named configuration. The main menu/deployment system stores the selected loadout and applies it before the jet is spawned.

## Ammo and Pylon Visuals

`UJetPylonVisualsComponent` keeps the external stores synchronized with the runtime loadout.

Important behavior:

- disabled weapons are hidden
- missile and rocket meshes are hidden when their ammo reaches zero
- respawn/reload reapplies the current runtime state
- pylon visuals are presentation only; the server weapon state remains authoritative

When adding a new pylon, configure its mesh reference and weapon association in the aircraft Blueprint. Do not infer ammunition from mesh visibility.

## Gun System

The gun supports Blueprint-editable categories for:

- damage, range, spread, and fire timing
- tracer class and spawn behavior
- weapon state, cooldown, and overheating
- cockpit/shoulder, chase, and remote audio
- release-tail sound with minimum fire time and anti-spam cooldown

Remote gun audio uses distance checks and attenuation so nearby players hear the exterior weapon without receiving cockpit audio.

## Rockets

Rockets are unguided and use the firing aircraft's current transform and velocity-aware launch handling. Configure rocket class, ammo, cadence, damage, FX, and audio on `UJetWeaponComponent`.

In multiplayer, the owning client requests fire and the authoritative path creates the gameplay projectile. Local presentation compensates for fast aircraft motion so rockets do not appear to originate behind the jet.

## Missiles

Missile launch requires a valid lock. The system supports:

- missile class and ammo
- lock validation
- homing target assignment
- launch safety and initial clearance
- speed/velocity inheritance
- trail and impact effects
- warning audio and countermeasure interaction

Missile gameplay is authoritative. Cosmetic feedback may begin locally, but damage and replicated projectile state are not client-owned.

## Flares

Flares are defensive countermeasures with configurable ammo, cooldown, launch transform, FX, and audio.

Player and AI flare sounds use spatial attenuation and remote audible-distance limits. If a flare is audible from too far away, verify both the assigned Sound Attenuation asset and the remote distance on the jet audio settings.

## Automatic Targeting

Automatic targeting uses `UJetTargetingComponent` and the forward aircraft view. It supports line trace or sphere sweep through `EJetTargetTraceMode`.

Default controls:

| Action | Default input |
|---|---|
| Toggle automatic targeting | T |
| Cycle next target | 1 |
| Cycle previous target | 2 |

Automatic mode provides the target widget and lock audio feedback. It supports aircraft, `AirTGT`, `GroundTGT`, and other valid radar/target actors.

## Manual Targeting

Manual targeting is a separate workflow owned by `UJetManualTargetingComponent`.

Default controls:

| Action | Default input |
|---|---|
| Enter/leave manual targeting | 3 |
| Toggle manual lock | 4 |

Manual mode uses the cockpit capture/TAD presentation. Its categories include:

- capture component and render filtering
- TAD screen configuration
- manual aim and focus
- target lock rules
- zoom and performance settings

### Clean Mode Separation

Automatic and manual targeting are mutually exclusive presentation modes:

- automatic mode uses the forward target widget and lock audio
- manual mode uses the TAD/capture workflow
- entering manual mode suppresses automatic lock UI and automatic targeting audio
- leaving manual mode restores the normal automatic-targeting state when allowed

This prevents a hidden automatic widget from leaving lock audio active during manual targeting.

## Adding a Weapon

For a new weapon type:

1. Create the authoritative projectile or trace implementation.
2. Add ammo and runtime state to `UJetWeaponComponent`.
3. Add a loadout flag/count if the weapon is selectable.
4. Add pylon visual mappings.
5. Add cockpit, chase, and remote audio with attenuation.
6. Add HUD feedback without making the HUD authoritative.
7. Test standalone, listen server, joined client, respawn, and ammo depletion.

## Multiplayer Checklist

- Only the owning player sends fire input.
- The server validates and owns gameplay damage.
- Remote audio is spatial and distance-limited.
- Projectiles remain visually attached to the launch point at high speed.
- Ammo and pylon visibility remain correct after respawn.
- A client cannot fire a disabled or empty weapon.

## Screenshot Placeholders

- Weapon component Details panel
- Loadout preset array
- Automatic lock UI
- Manual TAD targeting
- Pylon visuals before and after ammo depletion

See also: [Inputs](INPUTS.md), [HUD and Radar](HUD_AND_RADAR.md), and [AI System](AI_SYSTEM.md).
