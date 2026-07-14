# Input & Controls Guide

## Default Keyboard & Mouse Controls

Aerial Thunder includes complete default input mappings. These are example mappings—developers can call exposed C++ and Blueprint functions from Enhanced Input or any custom input system.

---

## Flight Controls

| Function | Default Input | Type |
|----------|---------------|------|
| **Throttle Up** | Left Shift | Axis |
| **Throttle Down** | Left Ctrl | Axis |
| **Pitch Up** | W | Axis |
| **Pitch Down** | S | Axis |
| **Roll Left** | A | Axis |
| **Roll Right** | D | Axis |
| **Yaw Left** | Q | Axis |
| **Yaw Right** | E | Axis |
| **Air Brake** | Space | Action (Toggle/Hold) |
| **Ground Brake** | Space (on ground) | Action (Hold) |
| **Auto Level** | H | Action (Press) |
| **Start Engine** | Enter | Action (Press) |
| **Toggle Landing Gear** | G | Action (Press) |

---

## Camera Controls

| Function | Default Input | Type |
|----------|---------------|------|
| **Change Camera** | V | Action (Press) |
| **Camera Reset** | 5 or Middle Mouse | Action (Press) |
| **Camera Zoom In** | Mouse Wheel Up | Axis |
| **Camera Zoom Out** | Mouse Wheel Down | Axis |
| **Look Left** | Mouse X (negative) | Axis |
| **Look Right** | Mouse X (positive) | Axis |
| **Look Up** | Mouse Y (negative) | Axis |
| **Look Down** | Mouse Y (positive) | Axis |

---

## Weapon Controls

| Function | Default Input | Type |
|----------|---------------|------|
| **Fire Gun** | Left Mouse Button | Action (Hold/Repeat) |
| **Fire Rockets** | Right Mouse Button | Action (Press) |
| **Fire Missile** | Middle Mouse Button | Action (Press) |
| **Deploy Flares** | X | Action (Hold/Repeat) |

---

## Targeting Controls

| Function | Default Input | Type |
|----------|---------------|------|
| **Auto Targeting** | T | Action (Toggle) |
| **Next Target** | 1 | Action (Press) |
| **Previous Target** | 2 | Action (Press) |
| **Manual Targeting** | 3 | Action (Press) |
| **Manual Target Lock** | 4 | Action (Press) |

---

## Warning & System Controls

| Function | Default Input | Type |
|----------|---------------|------|
| **Warning System** | K | Action (Toggle) |
| **Pause Game** | Escape or P | Action (Press) |
| **Scoreboard** | Tab | Action (Press/Hold) |
| **Multiplayer Dashboard** | U | Action (Press) |
| **Skip Mission Intro** | Space | Action (Press) |

---

## Input System Architecture

### Default Input System (Legacy)
Aerial Thunder ships with **Default Input System** bindings. These are configured in:
```
Project Settings → Engine → Input
```

**Axis Mappings** (continuous values):
- `MoveForward` — W (+1) / S (-1)
- `MoveRight` — A (-1) / D (+1) *Note: In aviation, this controls roll, not strafe*
- `LookUp` — Mouse Y
- `LookRight` — Mouse X
- `Throttle` — Left Shift (+1) / Left Ctrl (-1)
- `Yaw` — Q (-1) / E (+1)
- `CameraZoom` — Mouse Wheel

**Action Mappings** (discrete events):
- `Brake`
- `StartEngine`
- `LandingGear`
- `AutoLevel`
- `ChangeCamera`
- `CameraReset`
- `FireGun`
- `FireRockets`
- `FireMissile`
- `DeployFlares`
- `AutoTargeting`
- `NextTarget`
- `PreviousTarget`
- `ManualTargeting`
- `ManualTargetLock`
- `WarningSystem`
- `Pause`
- `Scoreboard`
- `MultiplayerDashboard`
- `SkipMissionIntro`

---

## Using Enhanced Input System

If you prefer the **Enhanced Input System** (recommended for new projects):

### Setup
1. **Enable Enhanced Input Plugin**
   - Edit → Plugins → Search "Enhanced Input" → Enable
   - Restart the editor

2. **Create Input Map Context** (IA) and **Input Actions** (IA)
   - Content Browser → Content / Input /
   - Right-click → Miscellaneous → Input Mapping Context
   - Create one per gameplay state (Flight, Menu, etc.)

3. **Map Player Controller to Enhanced Input**
   - In your player controller Blueprint:
     - Set `Enhanced Input System Component`
     - Load your Input Mapping Context on Possess

### Example Setup (TODO: Verify actual paths and naming in project)

#### Input Action: IA_Pitch
```
Value Type: Axis1D (Float)
Bindings:
  - W Key → Value +1.0
  - S Key → Value -1.0
```

#### Input Action: IA_FireGun
```
Value Type: Digital (Boolean)
Bindings:
  - Left Mouse Button
```

#### Input Mapping Context: IMC_Flight
```
Mappings:
  IA_MoveForward → IA_Pitch
  IA_MoveRight → IA_Roll
  IA_LookUp → Mouse Y-Axis
  IA_LookRight → Mouse X-Axis
  IA_Throttle → Shift/Ctrl
  IA_FireGun → Left Mouse
  ... (etc for all actions)
```

#### In Your Aircraft Blueprint
```
Event: Setup Input Component
  └─ Bind Input Action IA_Pitch
      └─ Call MoveForward(Value)
  └─ Bind Input Action IA_FireGun
      └─ Call FireGun()
```

---

## Custom Input Implementation

You can also implement your own input system by calling the exposed Aircraft functions directly:

### Core Aircraft Functions

#### Flight Control
```cpp
// Called from any input system
void MoveForward(float AxisValue);     // Pitch control: -1.0 to +1.0
void MoveRight(float AxisValue);       // Roll control: -1.0 to +1.0
void LookYaw(float AxisValue);         // Yaw control: -1.0 to +1.0
void SetThrottle(float Value);         // Throttle: 0.0 to 1.0
void SetBrake(bool bActive);
void ToggleLandingGear();
void AutoLevel();
void StartEngine();
```

#### Camera Control
```cpp
void ChangeCamera();                   // Cycle through cameras
void CameraReset();                    // Reset to default zoom/angle
void CameraZoom(float AxisValue);      // Zoom: -1.0 to +1.0
void CameraLook(FVector2D LookInput);  // Look direction
```

#### Weapons
```cpp
void FireGun(bool bPressed);           // Gun fire: hold or repeat
void FireRockets();                    // One rocket per call
void FireMissile();                    // One missile per call
void DeployFlares(bool bActive);       // Flare deployment: hold or repeat
```

#### Targeting
```cpp
void AutoTargeting();                  // Toggle automatic lock
void NextTarget();                     // Cycle to next target
void PreviousTarget();                 // Cycle to previous target
void ManualTargeting();                // Enter manual targeting mode
void ManualTargetLock();               // Lock onto manual target
```

---

## Input Timing & Feedback

### Responsiveness
- **Flight Input:** Immediately reflected in aircraft rotation (client-side prediction)
- **Weapon Fire:** Registered on client, confirmed on server (latency ≈ network ping)
- **Targeting:** Auto-lock calculations updated at 10 Hz (configurable)
- **Camera:** Immediate client-side response

### Anti-Cheat Considerations
- All damage and elimination decisions are **server-authoritative**
- Client input is used for movement, server validates physics
- Weapon fire is replicated with server confirmation
- Impossible moves (out-of-bounds input) are rejected by server

---

## Gamepad Support

Gamepad input is supported via the Default Input System:

### Recommended Gamepad Mapping

| Function | Gamepad Input |
|----------|---------------|
| **Pitch** | Right Thumbstick Y |
| **Roll** | Right Thumbstick X |
| **Yaw** | Left Trigger + Right Trigger (shoulder) |
| **Throttle** | Left Thumbstick Y (forward/back) |
| **Fire Gun** | Right Trigger (RT) |
| **Fire Rockets** | Left Shoulder (LB) |
| **Fire Missile** | Right Shoulder (RB) |
| **Deploy Flares** | A Button |
| **Change Camera** | Y Button |
| **Pause** | Start Button |

**Note:** TODO: Verify gamepad binding configuration in project.

---

## Mobile/Touch Input (if applicable)

TODO: Verify if touch input is supported. If not, add note.

---

## Input Validation & Limits

### Input Ranges
- **Axis Values:** -1.0 to +1.0 (normalized)
- **Throttle:** 0.0 (off) to 1.0 (full power)
- **Brakes:** Boolean (0 or 1)

### Input Filtering
- **Dead Zone:** Small inputs near zero are ignored (prevents drift)
- **Scaling:** Inputs are scaled by sensitivity settings (see [Settings Reference](SETTINGS_REFERENCE.md))
- **Rate Limiting:** Rapid repeated inputs are filtered to prevent exploits

---

## Troubleshooting Input Issues

### Controls Don't Respond
1. **Ensure focus:** Click in the game window
2. **Check pause state:** Press Escape to unpause
3. **Verify input bindings:** Edit → Project Settings → Input
4. **Check input component:** In Blueprint, verify "Setup Input Component" is called

### Inputs Are Too Sensitive / Not Responsive Enough
1. **Adjust sensitivity:** Main Menu → Settings → Controls
2. **Check dead zone:** Project Settings → Input → Axis Properties
3. **Verify scaling:** See [Settings Reference](SETTINGS_REFERENCE.md)

### Gamepad Not Detected
1. **Test in Windows:** Settings → Devices → Game controllers
2. **Restart editor:** Plug in gamepad, restart editor
3. **Check mapping:** Verify gamepad binding in Project Settings

### Enhanced Input Not Working
1. **Verify plugin enabled:** Edit → Plugins → "Enhanced Input"
2. **Check setup:** Ensure Input Mapping Context is loaded in PlayerController
3. **Verify bindings:** Check IA and IMC assets for correct mappings
4. **Check focus:** Ensure PlayerController has Input Component enabled

---

## Best Practices

1. **Use Enhanced Input for new projects** — More flexible and better supported
2. **Bind only when needed** — Unbind inputs when not in use (e.g., pause menu)
3. **Test on target input device** — Keyboard + mouse, gamepad, or custom input
4. **Use input sensitivity settings** — Allow players to customize responsiveness
5. **Provide key rebinding UI** — Let players customize controls to their preference
6. **Test latency** — Verify input responsiveness with network lag

---

For more details, see:
- [Flight & Cameras](FLIGHT_AND_CAMERAS.md) — Flight-specific input handling
- [Weapons & Targeting](WEAPONS_AND_TARGETING.md) — Weapon input patterns
- [Multiplayer](MULTIPLAYER.md) — Input replication and netcode
- [Settings Reference](SETTINGS_REFERENCE.md) — Input sensitivity and configuration
