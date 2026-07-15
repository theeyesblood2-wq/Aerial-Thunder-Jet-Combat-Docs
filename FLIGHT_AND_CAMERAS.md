# Flight and Cameras Guide

## Overview

Aerial Thunder provides a configurable jet flight system built for both immediate arcade-style play and more demanding handling. Flight, ground movement, takeoff, landing assistance, camera behavior, and multiplayer movement are implemented by the `Jet_C_MT` plugin.

The supplied jet Blueprint exposes the important tuning values in the Details panel. Projects can adjust handling without rewriting the core C++ systems.

## Control Presets

The jet supports four runtime control presets:

| Preset | Intended feel |
|---|---|
| Arcade | Fast response and stronger assistance |
| Normal | Accessible general-purpose handling |
| Advanced | Faster, less forgiving combat handling |
| Realsim | The most demanding supplied configuration |

The example main menu presents the player-facing choices configured for the sample game. Developers can expose more presets or change their tuning in Blueprint.

Each preset can independently modify movement, rotation rates, damping, input smoothing, recovery assistance, ground behavior, takeoff behavior, crash damage, targeting availability, and ammo rules.

## Default Flight Controls

| Action | Default input |
|---|---|
| Throttle up | Left Shift |
| Throttle down | Left Ctrl |
| Pitch | W / S |
| Roll | A / D |
| Yaw | Q / E |
| Air brake / brake | Space |
| Auto-level | H |
| Landing gear | G |

See [INPUTS.md](INPUTS.md) for the complete input list and integration notes.

## Airborne Flight

The movement component handles acceleration, deceleration, pitch, yaw, roll, damping, bank-to-turn response, and input smoothing. These values are configurable and may differ between presets.

### Auto-Level

Auto-level is an optional recovery assist. It can help return the aircraft toward stable flight after player input is released. Its strength, delay, pitch recovery, roll recovery, interpolation speed, minimum speed, and throttle response can be tuned per preset.

### Air Brake

The air brake reduces speed and helps with overshoot, landing setup, and defensive maneuvers. It is not a substitute for planning the approach at the jet's current speed.

### High-Speed Handling

The included jet is intentionally fast. Avoid documenting fixed top speeds or turn rates as product guarantees because the supplied Blueprint values and control presets are editable.

## Ground Start and Airborne Start

The jet supports two startup modes:

- `Grounded`: use for runway or carrier starts.
- `Airborne`: use when the aircraft should begin already in flight.

The mission and deployment systems can select the appropriate spawn point and startup mode. Ground movement has separate steering, acceleration, deceleration, braking, and takeoff tuning.

## Landing Gear and Landing Assist

Press `G` to toggle the landing gear.

The gear system includes a Blueprint-editable input cooldown so repeated key presses do not spam the gear state or gear audio. When configured, lowering the gear also activates landing assistance.

Landing assistance can:

- reduce the aircraft's effective speed for approach,
- smooth pitch, roll, and yaw response,
- make runway and carrier alignment more manageable,
- preserve the project's selected control preset outside the landing state.

The assist is triggered by the gear state. It does not require a separate player input.

### Suggested Landing Procedure

1. Align with the runway, carrier, or configured landing area early.
2. Reduce throttle before the final approach.
3. Lower the landing gear.
4. Use small pitch, roll, and yaw corrections.
5. Use the air brake when additional speed reduction is needed.
6. Touch down as straight and level as possible.

Landing detection uses the project's configured collision and trace setup. Verify custom surfaces after changing collision channels.

## Camera System

Three player camera views are supplied:

| Camera | Use |
|---|---|
| Cockpit | First-person flight, HUD, manual targeting, and immersion |
| Shoulder | Close external view with aircraft context |
| Chase | Wider external combat view |

### Default Camera Controls

| Action | Default input |
|---|---|
| Cycle camera | V |
| Reset camera | 5 |
| Look | Mouse |
| Zoom | Mouse wheel |

Camera offsets, boom behavior, field of view, look response, zoom limits, and view-specific audio behavior are configurable in the jet Blueprint.

## Camera and Audio Context

The audio system distinguishes cockpit/shoulder, chase, and remote aircraft playback where appropriate. This allows the local pilot and nearby players to hear different versions or volumes of engine and weapon sounds.

Do not play local cockpit audio as a replicated global sound. Remote weapon and flyby audio should remain distance-gated and spatialized.

## Multiplayer Movement

The jet uses server-authoritative multiplayer movement with client and simulated-proxy smoothing. The project includes tuning for correction, interpolation, and high-speed visual stability.

Important expectations:

- The owning player should receive responsive local flight.
- Other players see replicated and smoothed aircraft movement.
- Real internet latency can still produce small visible delay, especially during close high-speed passes.
- Test both host and joined-client views before changing network smoothing values.

Network tuning is documented further in [MULTIPLAYER.md](MULTIPLAYER.md).

## Crash and Recovery

Crash damage is configurable per control preset. The game framework handles destruction, killed-in-action presentation, spectating, countdown, and respawn.

The sample project supports:

- collision and fatal-impact handling,
- single-player and multiplayer destruction,
- killer spectating through a world camera,
- respawn after the killed-in-action countdown.

## Blueprint Configuration Areas

Look in the jet Blueprint for these groups:

- `Jet | Control Presets`
- `Movement`
- `Ground`
- `Assist`
- `Gameplay`
- camera settings
- landing gear and landing assist settings
- multiplayer movement and smoothing settings

Names and grouping may vary slightly in derived Blueprints.

## Troubleshooting

### The jet is too sensitive

- Try the Arcade or Normal preset.
- Lower pitch, yaw, and roll multipliers in the selected preset.
- Increase input smoothing or damping.
- Confirm the root menu applies the intended control preset before spawn.

### The jet is difficult to land

- Lower the gear early enough for the assist to take effect.
- Reduce throttle before reaching the runway.
- Verify landing assist is enabled in the jet Blueprint.
- Check the landing surface collision channel.

### The gear or gear sound repeats

- Increase the Blueprint-editable gear toggle cooldown.
- Confirm no second Blueprint input path calls the same gear function.

### A remote jet shakes

- Test in a packaged host/client session.
- Lock both clients to a stable frame rate for comparison.
- Check latency and packet conditions before changing smoothing.
- Avoid running duplicate Blueprint movement logic on simulated proxies.

### The camera feels wrong after customization

- Reset the view with `5`.
- Verify the selected camera's offset, FOV, and look settings.
- Check that only the locally controlled jet processes player camera input.

## Related Guides

- [INPUTS.md](INPUTS.md)
- [HUD_AND_RADAR.md](HUD_AND_RADAR.md)
- [WEAPONS_AND_TARGETING.md](WEAPONS_AND_TARGETING.md)
- [MULTIPLAYER.md](MULTIPLAYER.md)
- [SETTINGS_REFERENCE.md](SETTINGS_REFERENCE.md)
