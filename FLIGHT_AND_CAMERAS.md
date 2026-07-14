# Flight and Cameras

This guide covers the player aircraft movement, control presets, ground handling, landing assistance, and the three included camera views.

## Core Classes

The flight stack belongs to the `Jet_C_MT` plugin:

- `AJetPawn` owns the aircraft, input bridge, cameras, gear, assists, warnings, and replicated presentation.
- `UJetMovementComponent` simulates airborne movement.
- `UJetGroundMovementComponent` handles taxi, braking, steering, and takeoff transition.
- `UJetAnimInstance` exposes aircraft animation values to the Animation Blueprint.

`AT_GM` selects and spawns the aircraft, but it does not own the flight simulation.

## Control Presets

`EJetControlPreset` provides four runtime presets:

| Preset | Intended use |
|---|---|
| Arcade | Accessible handling with stronger assistance. |
| Normal | Balanced handling for general play. |
| Advanced | Faster, more demanding handling with reduced assistance. |
| Realsim | The most simulation-oriented configuration. |

Presets are applied through the jet runtime configuration. Keep per-aircraft tuning in the Jet Blueprint and let the game/menu layer select the preset.

## Airborne Movement

Select the jet's `JetMovementComponent` to tune the flight model. The Details panel groups settings into practical categories including:

- flight speed, acceleration, drag, turn response, lift, and stall behavior
- pitch, roll, yaw, and throttle response
- automatic level recovery
- air-brake and idle-fall behavior
- uncontrolled/destroyed movement

The player and `UJetAIPilotComponent` both feed the same movement path. This is important for consistent aircraft behavior and replication.

### Default Flight Inputs

| Action | Default input |
|---|---|
| Throttle up / down | Left Shift / Left Ctrl |
| Pitch | W / S |
| Roll | A / D |
| Yaw | Q / E |
| Air brake | Space Bar |
| Auto level | H |
| Start engine | Enter |

Input mappings are defined in `Config/DefaultInput.ini`. They can be replaced or extended in the project without changing the plugin's flight code.

## Startup Modes

`EJetStartupMode` supports:

- `Grounded`
- `Airborne`

Use the correct mode for the spawn point. A grounded start initializes taxi/takeoff behavior; an airborne start initializes the aircraft directly into flight.

## Ground Handling and Takeoff

`UJetGroundMovementComponent` provides Blueprint-editable values for:

- maximum ground speed
- acceleration and deceleration
- braking force
- steering/yaw rate
- takeoff throttle threshold
- takeoff speed threshold
- launch upward speed

The default project includes separate forward movement, steering, braking, gear, and takeoff behavior. Avoid moving this logic into a level Blueprint; configure the component on the aircraft Blueprint instead.

## Landing Gear and Landing Assist

The jet exposes dedicated `Gear`, `Gear Audio`, `Landing Assist`, and `Gear Down Approach` categories.

Gear-down behavior can provide:

- a controlled approach speed
- smoother pitch, roll, and yaw response
- landing-area trace support
- configurable transition/cooldown behavior
- one-shot gear up/down audio

The gear toggle has a cooldown so repeated input cannot spam the gear animation or sound.

Default gear input: `G`.

## Camera Views

The project includes three camera components and runtime view switching:

| View | Purpose |
|---|---|
| Cockpit | First-person pilot view with cockpit HUD and limited head look. |
| Shoulder | Close third-person aircraft view. |
| Chase | Distant third-person view with zoom and optional free look. |

Default view input: `V`.

### Cockpit View

Cockpit settings are under `View|Cockpit`. The jet exposes independent yaw, pitch-up, pitch-down, and look-speed limits.

Cockpit-only presentation can include:

- cockpit HUD and tactical displays
- pilot helmet visibility rules
- pitch cue arrows
- acceleration, roll, pitch, landing, and shake camera feedback
- rain and canopy water effects

### Shoulder View

The shoulder camera uses its own anchor and camera component. It can receive camera feedback separately from cockpit and chase views, so the close exterior view can feel responsive without changing aircraft movement.

### Chase View

Chase options are under `View|Chase` and include:

- allow look
- world-stable free look
- follow jet yaw
- optional yaw limit
- pitch limits and look speed

The chase camera is mounted to a spring arm and supports smooth distance changes.

### Zoom and Reset

Zoom settings are under `View|Zoom`:

- chase arm minimum/maximum length
- arm interpolation speed
- cockpit and chase FOV ranges
- FOV interpolation speeds
- mouse-wheel step values

| Action | Default input |
|---|---|
| Zoom | Mouse Wheel |
| Reset camera | 5 |

## Camera Feedback

Cockpit and shoulder feedback is visual only. It uses aircraft velocity and rotation to add local camera motion while leaving the replicated aircraft transform untouched. This separation prevents camera polish from changing multiplayer flight authority.

Tune camera shake conservatively for high-speed flight. Test cockpit, shoulder, and chase independently after changing any feedback values.

## Multiplayer Notes

- The server remains authoritative over aircraft movement.
- The owning player receives responsive local presentation.
- Remote jets use buffered interpolation and proxy presentation smoothing.
- Camera movement is local and is not replicated to other players.
- Do not drive replicated jet movement from a camera or Animation Blueprint.

## Recommended Test Pass

After changing flight or camera settings, verify:

1. Grounded engine start, taxi, brake, and takeoff.
2. Airborne spawn and immediate control.
3. Pitch, roll, yaw, throttle, auto level, and air brake.
4. Gear-down approach and landing.
5. Cockpit, shoulder, and chase switching.
6. Zoom and camera reset in every view.
7. Listen-server and joined-client movement at slow nearby flight and high speed.

## Screenshot Placeholders

- Jet Blueprint flight component settings
- Control preset selection
- Cockpit, shoulder, and chase comparison
- Landing assist and gear categories

See also: [Inputs](INPUTS.md), [Architecture](ARCHITECTURE.md), and [HUD and Radar](HUD_AND_RADAR.md).
