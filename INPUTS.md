# Input and Controls Guide

## Overview

Aerial Thunder ships with keyboard, mouse, and Xbox-compatible gamepad mappings in `Config/DefaultInput.ini`. Gameplay uses the existing named action/axis mappings through Enhanced Player Input classes. Players can change these mappings at runtime from **Root Menu > Settings > Key Bindings**.

Developers can change packaged defaults in:

```text
Edit > Project Settings > Engine > Input
```

---

## Flight Controls

| Function | Default Input | Mapping Name |
|----------|---------------|--------------|
| Throttle up | Left Shift | `Throttle` (+1) |
| Throttle down | Left Ctrl | `Throttle` (-1) |
| Pitch up | W | `Pitch` (+1) |
| Pitch down | S | `Pitch` (-1) |
| Roll left | A | `Roll` (-1) |
| Roll right | D | `Roll` (+1) |
| Yaw left | Q | `Yaw` (-1) |
| Yaw right | E | `Yaw` (+1) |
| Air brake | Space | `AirBrake` |
| Ground brake | Space | `Brake` |
| Auto level | H | `AutoLevel` |
| Start engine | Enter | `StartEngine` |
| Landing gear up/down | G | `JetGearUP` |
| Dogfight assist | Z | `JetDogFight` |

The shared Space key is intentional. Its effect depends on whether the jet is airborne, grounded, or playing a skippable mission intro.

---

## Camera Controls

| Function | Default Input | Mapping Name |
|----------|---------------|--------------|
| Change camera | V | `ToggleView` |
| Reset camera | 5 | `CameraReset` |
| Look horizontally | Mouse X | `LookRight` / `Turn` |
| Look vertically | Mouse Y | `LookUp` |
| Zoom | Mouse wheel | `ZoomInOut` |

The jet supports cockpit, shoulder, and chase camera views. Camera behavior also depends on the selected control and camera settings.

---

## Weapons

| Function | Default Input | Mapping Name |
|----------|---------------|--------------|
| Fire gun | Left Mouse Button | `FireGun` |
| Fire rocket | Right Mouse Button | `FireRocket` |
| Fire missile | Middle Mouse Button | `JetFireMissile` |
| Deploy flares | X | `DeployFlares` |

Weapon availability depends on the selected loadout and remaining ammunition. Pylon visuals update with the current missile and rocket ammunition state.

---

## Targeting

| Function | Default Input | Mapping Name |
|----------|---------------|--------------|
| Toggle auto targeting | T | `Targeting` |
| Next target | 1 | `CycleTargetNext` |
| Previous target | 2 | `CycleTargetPrevious` |
| Enter manual targeting | 3 | `ManualTargeting` |
| Toggle manual lock | 4 | `ManualTargetToggle` |

Auto and manual targeting are separate modes:

- **Auto targeting** uses the forward targeting workflow, lock widget, and lock audio.
- **Manual targeting** uses the cockpit capture/TAD workflow and suppresses the automatic lock widget and audio.

---

## Game and Multiplayer Controls

| Function | Default Input | Mapping Name |
|----------|---------------|--------------|
| Warning system | K | `JetWarningSystem` |
| Pause menu | Escape or P | `PauseMenu` |
| Team Death Match scoreboard | Tab | `TDMScoreboard` |
| Multiplayer dashboard toggle | U | `TDMScoreboardToggle` |
| Skip mission intro | Space | `SkipMissionIntro` |
| Show/hide controls guide | 8 | `Guide` |

Mission intro skipping only works when the active mission intro director allows skipping and a playable intro is running.

---

## Input Configuration

The exact shipped mapping names matter because the C++ and Blueprint gameplay classes listen for them. If you rename a mapping, update every listener that uses that name.

Recommended workflow:

1. Duplicate the project before changing the default control scheme.
2. Open **Project Settings > Input**.
3. Change keys while keeping the existing mapping names.
4. Test airborne start, grounded start, every camera, targeting modes, and pause/menu input.
5. Test both a standalone session and a two-player listen-server session.

### Runtime Key Bindings

The root Settings screen creates one row per packaged action/axis definition. Each row provides independent **Primary** and **Secondary** slots.

- Select a slot, then press a keyboard, mouse, gamepad button, trigger, or analog-stick direction.
- Analog capture uses an arm delay and threshold so stick drift does not immediately select an axis.
- Duplicate-key validation rejects conflicting assignments.
- **Apply Settings** changes the current session.
- **Save Settings** persists local overrides in the `AT_GM_InputBindings` save slot.
- Right-click a populated slot to reset only that slot.
- **Reset Bindings** restores the complete packaged keyboard/mouse/gamepad layout.
- Overrides are local-player data and are never replicated to other multiplayer players.
- Bindings are reapplied after travel when the LocalPlayer receives a new PlayerController.

The supplied editor is available from the root menu before gameplay. Pause-menu key-binding integration is intentionally not included in the current checkpoint.

### Mouse Sensitivity

The supplied input configuration uses a sensitivity of `0.07` for Mouse X, Mouse Y, and Mouse 2D. Player-facing control settings can further affect the feel of camera and flight input.

### Xbox-Compatible Gamepad Defaults

| Function | Default gamepad input |
|---|---|
| Pitch / Roll | Left Stick Y / X |
| Camera Look | Right Stick Y / X |
| Throttle Down / Up | Left / Right Trigger |
| Yaw Left / Right | Left / Right Shoulder |
| Gun / Rocket / Missile | Bottom / Right / Left Face Button |
| Auto Targeting | Top Face Button |
| Manual Targeting / Toggle | D-pad Up / Right |
| Gear / Guide | D-pad Down / Left |
| Toggle View / Flares | Left / Right Thumbstick Button |
| Camera Reset | Special Left |

Generic Unreal `Gamepad_*` keys support Xbox One, Xbox Series, Elite, and normal XInput-compatible devices. Same-PC packaged tests use `Slate.RequireFocusForGamepadInput=1`; only the focused game window receives the physical controller.

PS4/PS5 and HOTAS support is not guaranteed by this checkpoint. The binding UI can capture any `FKey` delivered by Unreal, but the device still requires a stable Windows/Unreal input backend. HOTAS devices commonly need Raw Input plus device-specific calibration, deadzones, and axis testing.

### Migrating to Input Actions and Mapping Contexts

Developers may replace the named mappings with a full Enhanced Input action/context setup. This is an integration task, not a prebuilt asset set included with the template. Preserve the same gameplay intent and call the existing jet/controller interfaces from the new input events.

---

## Troubleshooting

### No Flight Input

1. Click the game viewport so it has focus.
2. Confirm the game is not paused or displaying a modal menu.
3. Confirm the player controller possesses the expected jet pawn.
4. Check that the mapping names still match `DefaultInput.ini`.
5. For mission intros, wait for possession or use the configured skip workflow.

### Wrong Key Behavior

Some keys intentionally serve more than one context. Space can brake, air-brake, or skip an intro. Verify the current grounded/airborne and mission state before changing the mapping.

### Camera Does Not Move

1. Confirm the active camera view permits free look.
2. Check `LookRight`, `LookUp`, and `ZoomInOut` mappings.
3. Reset the camera with 5.
4. Check the selected camera and control settings in the root menu.

### Input Feels Delayed Online

Compare the same action in standalone, local listen-server, and public EOS sessions. Joined-client responsiveness can be affected by network latency and packet timing; do not tune offline flight behavior from one poor internet test.

---

## Related Guides

- [Flight and Cameras](FLIGHT_AND_CAMERAS.md)
- [Weapons and Targeting](WEAPONS_AND_TARGETING.md)
- [Multiplayer](MULTIPLAYER.md)
- [Settings Reference](SETTINGS_REFERENCE.md)
