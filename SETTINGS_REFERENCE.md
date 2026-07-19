# Settings Reference

Aerial Thunder stores player-facing configuration through the AT_GM settings system. The root settings UI includes Graphics, Audio, Visual, Controls, Key Bindings, UI, and Profile sections.

This page documents settings that exist in the supplied project. Jet component tuning is covered by the system-specific guides because those values belong to Jet_C_MT Blueprint components rather than the root user-settings save.

## Profile

| Setting | Type | Limit | Purpose |
|---|---|---:|---|
| Player Display Name | Text | 16 characters | Pilot name used by menus and multiplayer identity |
| Player Region | Text | 32 characters | Region stored with the player profile |
| Player Location | Text | 32 characters | Country/location stored with the player profile |

Input is length-limited while typing. Name and server-name validation also reject configured disallowed words.

## Graphics

| Setting | Values | Purpose |
|---|---|---|
| Resolution | Supported display resolutions | Output resolution |
| Window Mode | Fullscreen, Borderless, Windowed | Display mode |
| VSync | On/Off | Synchronize presentation to the display |
| Frame Rate Limit | `0` to `240` | `0` means uncapped |
| Graphics Quality | `0` to `4` | Overall quality preset |
| View Distance Quality | `0` to `4` | View-distance scalability |
| Shadow Quality | `0` to `4` | Shadow scalability |
| Effects Quality | `0` to `4` | Effects scalability |
| Post Process Quality | `0` to `4` | Post-process scalability |

## Visual

| Setting | Range/Values | Purpose |
|---|---|---|
| Gamma | `0.5` to `2.5` | Display brightness/gamma |
| Bloom | On/Off | Bloom post process |
| Motion Blur | On/Off | Motion-blur post process |
| Camera Shake | On/Off | Enables camera-shake feedback |
| Camera Shake Strength | `0.0` to `2.0` | Camera-shake intensity |
| Lens Flare | On/Off | Lens-flare post process |
| Jet Exhaust FX | See modes below | Selects the runtime exhaust presentation |

### Jet Exhaust FX modes

- Blueprint Default
- None
- Niagara
- Static Mesh + Material
- Niagara + Static Mesh + Material

The shipped default is **Static Mesh + Material**. This setting lets testers compare the combined effect against the lighter static-mesh path without rebuilding the project.

## Audio

| Setting | Purpose |
|---|---|
| Master Volume | Overall output volume |
| Music Enabled | Enables or disables music |
| Music Volume | Music level |
| SFX Volume | General sound-effects level |
| UI Volume | Interface sound level |
| Engine Volume | Jet engine sound level |
| Weapon Volume | Gun, rocket, missile, and related weapon level |

Volume values are normalized user settings. Individual jet and AI audio components also expose Blueprint-editable cue, attenuation, and category-specific volume controls.

## Controls

| Setting | Default/Range | Purpose |
|---|---|---|
| Control Mode | Advanced | Arcade, Normal, Advanced, or Realsim flight behavior |
| Mouse Sensitivity | `0.05` to `5.0` | Mouse-look/control sensitivity |
| Controller Sensitivity | `0.05` to `5.0` | Controller sensitivity |
| Controller Deadzone | `0.0` to `0.5` | Analog deadzone |
| Invert Pitch | On/Off | Inverts pitch input |
| Invert Yaw | On/Off | Inverts yaw input |

## Key Bindings

Runtime bindings expose Primary and Secondary slots for the packaged named action/axis mappings. Apply changes the current session, Save persists local overrides, Reset Bindings restores packaged defaults, and right-click resets one selected slot. Duplicate assignments are rejected. See [Input and Controls](INPUTS.md) for the complete workflow and Xbox-compatible defaults.

## UI

| Setting | Purpose |
|---|---|
| Show HUD | Shows the flight HUD |
| Show Target Markers | Shows supported target markers |
| Show Guide Window | Shows the project guide/control window |
| HUD Scale | Retained compatibility setting for HUD scale |
| Show HUD Help | Retained compatibility setting for HUD help |

The last two values remain in the saved data for backward compatibility. Their visible effect depends on the active project widget implementation.

## Saving and Applying

The settings screen provides separate reset, save, and apply actions. The project can restore saved profile and user settings on later launches.

For display or runtime-quality changes, use **Apply Settings** after editing. Use **Save Settings** to persist the selected values.

## Jet Blueprint Tuning

Jet_C_MT exposes a large set of component-owned options in the jet Blueprint. Important groups include:

- Flight handling and presets
- Grounded/airborne startup
- Camera feel and camera mode
- Landing gear and landing assist
- Engine exhaust presentation
- Gun, rockets, missiles, flares, and ammo
- Targeting and radar
- Warning system
- Water and cockpit-camera FX
- Network movement and smoothing
- AI pilot behavior and difficulty

These are not copied into the root user-settings save unless a specific UI bridge exists. See the dedicated documentation pages before changing them.

## Not Included

The project does not ship root settings for fuel capacity, fuel burn, engine overheating, ranked matchmaking, dedicated-server tuning, voice chat, or anti-cheat.

## Related Documentation

- [UI and Settings](UI_AND_SETTINGS.md)
- [Flight and Cameras](FLIGHT_AND_CAMERAS.md)
- [Weapons and Targeting](WEAPONS_AND_TARGETING.md)
- [HUD and Radar](HUD_AND_RADAR.md)
- [FX and Audio](FX_AND_AUDIO.md)
- [AI System](AI_SYSTEM.md)
