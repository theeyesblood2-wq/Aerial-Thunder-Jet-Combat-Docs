# Quick Start Guide

**Tested on:** Unreal Engine 5.7  
**Platform:** Windows / Win64  
**Project type:** C++

---

## Installation

### 1. Install the Required Tools

Install:

- Unreal Engine 5.7
- Visual Studio 2022
- Desktop development with C++
- Unreal Engine installer and tooling components in Visual Studio

### 2. Open the Project

1. Open `AT_JetMP.uproject`.
2. Select **Yes** if Unreal Engine asks to rebuild project modules.
3. Wait for C++ compilation and asset discovery to finish.
4. Restart the editor if Unreal Engine requests it after enabling a dependency.

Both included runtime plugins must be enabled:

- `AT_GM`
- `Jet_C_MT`

### 3. Open the Main Menu

The configured editor and game startup map is:

```text
/Game/AT_Games/AT_GM_Base/Maps/Map_MainMenu
```

Open that map and press **Play**.

---

## Create a Player Profile

On the first launch:

1. Select a region.
2. Enter a location name.
3. Enter a pilot username.
4. Save the profile.

The profile UI limits username and server-name length and rejects configured blocked words. Saved profile values are reused by menus, sessions, multiplayer player state, and the killed-in-action information card.

---

## Your First Flight

### Free Flight

From the main menu:

1. Open **Single Player**.
2. Select **Free Flight**.
3. Select an aircraft, loadout, map, and control mode.
4. Start the game.

### Basic Controls

| Action | Default input |
|---|---|
| Start engine | Enter |
| Throttle up / down | Left Shift / Left Ctrl |
| Pitch | W / S |
| Roll | A / D |
| Yaw | Q / E |
| Brake | Space |
| Auto level | H |
| Landing gear | G |
| Change camera | V |
| Reset camera | 5 |
| Camera zoom | Mouse wheel |

For every configured input, see [Input and Controls](INPUTS.md).

### Airborne Start

An airborne start spawns and possesses the selected jet in flight. Apply throttle, use gentle pitch and roll inputs, and press **H** when you want auto-level assistance.

### Grounded Start

For a grounded start:

1. Press **Enter** to start the engine.
2. Hold **Left Shift** to increase throttle.
3. Steer with yaw while on the ground.
4. Use **Space** for braking.
5. Pitch up after reaching takeoff speed.
6. Press **G** to raise the landing gear after takeoff.

### Landing

1. Reduce throttle before the approach.
2. Press **G** to lower the landing gear.
3. Use the landing assistance and smoother control response during approach.
4. Align with the runway, carrier, or configured landing surface.
5. Touch down gently and apply **Space** to brake.

Gear transitions and their audio are protected by a Blueprint-editable cooldown.

---

## First Combat

| Action | Default input |
|---|---|
| Fire gun | Left Mouse Button |
| Fire rockets | Right Mouse Button |
| Fire missile | Middle Mouse Button |
| Deploy flares | X |
| Toggle automatic targeting | T |
| Next / previous target | 1 / 2 |
| Toggle manual targeting | 3 |
| Manual target lock | 4 |
| Toggle warning system | K |

### Automatic Targeting

Automatic targeting uses the forward targeting workflow, target widget, and targeting audio. Toggle it with **T**, cycle targets with **1** and **2**, then fire a missile after a valid lock.

### Manual Targeting

Manual targeting is a separate cockpit workflow. Press **3** to switch modes and use **4** to control the manual lock. The automatic target widget and lock audio are suppressed while manual targeting is active.

---

## Missions

Aerial Thunder includes three extendable missions:

### Mission 01 - Flight Training

- Airborne introduction
- Training waypoint route
- Standard and more demanding waypoint sections
- Mission completion unlocks Mission 02

### Mission 02 - Takeoff and Landing Training

- Grounded start
- Takeoff and landing workflow
- Mission completion unlocks Mission 03
- Result screen can launch the next configured mission

### Mission 03 - Combat Mission

- Fade-in start without requiring a Level Sequence
- ATC and pilot radio sequence
- Entry waypoint
- Targets activated when the waypoint is passed
- AI combat, required target tracking, timer, and action music
- Mission success, failure, and result handling

Mission 03 demonstrates the reusable systems intended for Mission 04, Mission 05, and later custom missions.

---

## Local Multiplayer Test

Use multi-player PIE before testing over the internet:

1. Open an online gameplay map such as `Map_Online_A` or `Map_Online_B`.
2. Open the Play settings.
3. Set the number of players to 2.
4. Use a listen-server PIE configuration.
5. Start PIE and test host and joined-client behavior separately.

Test movement, slow nearby passes, weapons, flares, exhaust, elimination, spectating, and respawn from both windows.

---

## Private and Public Sessions

### Private Session Workflow

The provided private lobby supports hosting, finding, selecting, and joining sessions. The host can configure the map, region/location display, server name, team, and maximum player count through the supplied UI.

### Public EOS Workflow

Public internet multiplayer is optional and requires developer-owned EOS credentials.

Before testing public sessions:

1. Complete [EOS Setup](EOS_SETUP.md).
2. Confirm the active online subsystem is EOS.
3. Confirm EOS initializes successfully.
4. Complete local-player EOS login.
5. Restart the editor after changing EOS configuration.

When EOS is not ready, offline gameplay remains available and public Host/Join controls stay disabled with a setup status message.

---

## Common First-Run Issues

### Project Does Not Compile

- Confirm Unreal Engine 5.7 is installed.
- Confirm Visual Studio 2022 C++ and Unreal Engine components are installed.
- Right-click the `.uproject` and regenerate project files if required.
- Rebuild the editor target from Visual Studio or Unreal Build Tool.

### Input Does Not Respond

- Click the game viewport to give it focus.
- Confirm the pause menu is closed.
- Confirm the local player possesses the jet.
- Check `Config/DefaultInput.ini` or your replacement input bindings.

### Public Buttons Stay Disabled

This is expected when EOS is disabled, incomplete, still connecting, or login failed. Follow [EOS Setup](EOS_SETUP.md) and read the status message in the public multiplayer UI.

### A Packaged Build Behaves Differently

- Test with a Development package first.
- Inspect the packaged logs.
- Confirm every travel map is cooked.
- Confirm required Blueprint classes and maps are assigned.
- Confirm EOS artifacts match the current build when testing public multiplayer.

See [Troubleshooting](TROUBLESHOOTING.md) for deeper checks.

---

## Next Steps

- Learn all controls in [Input and Controls](INPUTS.md).
- Understand ownership in [Architecture Overview](ARCHITECTURE.md).
- Review jet handling in [Flight and Cameras](FLIGHT_AND_CAMERAS.md).
- Review combat in [Weapons and Targeting](WEAPONS_AND_TARGETING.md).
- Configure public multiplayer in [EOS Setup](EOS_SETUP.md).

---

Load the main menu, create a profile, and begin with Free Flight or Mission 01.
