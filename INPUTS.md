# Input and Controls Guide

## Overview

Aerial Thunder ships with keyboard and mouse mappings in `Config/DefaultInput.ini`. The project currently uses named action and axis mappings through Unreal's input settings. The default player input and input component classes are Enhanced Input classes, but the supplied gameplay bindings are the named mappings listed below.

You can change the keys in:

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

### Mouse Sensitivity

The supplied input configuration uses a sensitivity of `0.07` for Mouse X, Mouse Y, and Mouse 2D. Player-facing control settings can further affect the feel of camera and flight input.

### Gamepad and Custom Controllers

The supplied documentation does not claim a complete default gamepad layout. Unreal exposes gamepad axis configuration, but developers should add and test their own action and axis mappings for the target controller.

When adding a controller:

1. Reuse the existing mapping names where possible.
2. Add dead zones appropriate to the device.
3. Test pitch, roll, yaw, throttle, camera, weapons, and menu focus separately.
4. Verify behavior in multiplayer as both host and joined client.

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
