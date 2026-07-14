# Quick Start Guide

**Tested on:** UE 5.7 (C++ Project)  
**Platform:** Windows / Win64

---

## Installation (5 minutes)

### Step 1: Open the Project
1. Launch Unreal Engine 5.7
2. Open the **Aerial Thunder** project
3. Allow the editor to compile C++ modules if prompted (may take 2-5 minutes)
4. Wait for the editor to fully load

### Step 2: Verify Plugin Compilation
After the editor opens:
- Both `AT_GM` and `Jet_C_MT` plugins should be enabled
- Check **Edit → Plugins** and search for "Aerial" or "Jet"
- Both plugins should show as "Enabled"
- Restart the editor if you enabled them for the first time

### Step 3: First Launch
1. Navigate to **Content Browser**
2. In the top-right, enable **View Options → Show Plugin Content**
3. Browse to `AT_GM Content / Maps / MainMenu`
4. Double-click **MainMenu** to load it
5. Press **Play** in the editor toolbar

---

## Your First Flight (10 minutes)

### From Main Menu
1. **Single Player** → Select a mission or free flight map
2. Choose your **Aircraft** (default: F-16)
3. Select **Difficulty** (Normal is recommended for first flight)
4. Click **Start**

### In-Game Controls
| Action | Key |
|--------|-----|
| **Throttle Up** | Left Shift |
| **Throttle Down** | Left Ctrl |
| **Pitch** | W (up) / S (down) |
| **Roll** | A (left) / D (right) |
| **Yaw** | Q (left) / E (right) |
| **Brake** | Space |
| **Change Camera** | V |
| **Fire Gun** | Left Mouse Button |
| **Fire Rockets** | Right Mouse Button |
| **Pause** | Escape |

For the complete control list, see [Input & Controls](INPUTS.md).

### Basic Flight
1. **Start your engine:** Press **Enter**
2. **Take off:** Increase throttle with **Left Shift** while pitching up with **W**
3. **Level flight:** Press **H** for auto-level assistance
4. **Land:** Reduce throttle and lower the nose gently
5. **Deploy landing gear:** Press **G** before landing

### First Combat
1. **Find a target:** Look around with the mouse
2. **Auto-target:** Press **T** to lock onto the nearest enemy
3. **Fire gun:** Hold **Left Mouse Button**
4. **Fire rockets:** Press **Right Mouse Button** (one round per press)
5. **Evade:** Roll and pitch away, deploy flares with **X** if locked on

---

## Single-Player Campaign

### Missions
Aerial Thunder includes three complete campaign missions:
1. **Infiltration** — Scout and mark targets
2. **Defense** — Protect friendly assets
3. **Strike** — Destroy high-value targets

### Mission Progress
- Complete objectives shown in the cockpit HUD
- Watch for radio callouts and warnings
- Return to base or designated area to complete
- Results screen shows your performance
- Progress is saved automatically

### Difficulty Levels
- **Normal** — Recommended for learning
- **Advanced** — Challenging AI and tighter mission constraints
- **Ace** — Maximum difficulty with expert AI tactics

---

## Local Multiplayer (Editor)

### Setting Up a Local Match
1. In the editor, open any multiplayer map (e.g., `DogfightArena`)
2. In **Play Settings**, set **Number of Players** to 2 or more
3. Set **Net Mode** to **Play as Listen Server**
4. Click **Play**

The editor will spawn multiple players locally for testing.

### Private LAN Multiplayer
1. Build the project in Development Editor or Shipping
2. Run multiple instances on the same network
3. One player hosts (listens); others join via IP address
4. All gameplay is replicated and server-authoritative

---

## Public Multiplayer (EOS)

Public internet multiplayer requires Epic Online Services configuration.

**Before attempting public multiplayer:**
1. Review [EOS Setup](EOS_SETUP.md)
2. Configure your EOS credentials
3. Enable EOS in project settings
4. Restart the editor

Once configured:
1. From main menu, select **Multiplayer**
2. Choose **Public Match** (only available if EOS is configured)
3. Select region and game mode
4. Click **Join**

If public matchmaking is unavailable, EOS is not yet enabled. See [EOS Setup](EOS_SETUP.md).

---

## Common Issues

### Project Won't Compile
**Solution:** Ensure you have Visual Studio 2022 installed with C++ development tools. Restart the editor and retry.

### Game Crashes on Launch
**Solution:** Delete the `Intermediate` and `Binaries` folders. Reopen the project and recompile.

### Controls Don't Respond
**Solution:** Ensure the viewport is focused (click in the game window) and pause is not active (press Escape).

### Can't Join Multiplayer
**Solution:** Verify both players are on the same network and one is running as listen server. See [Troubleshooting](TROUBLESHOOTING.md).

### EOS Login Fails
**Solution:** Check your EOS configuration and restart the editor. See [EOS Setup](EOS_SETUP.md).

---

## Next Steps

- **Learn all controls** → [Input & Controls](INPUTS.md)
- **Understand the architecture** → [Architecture Overview](ARCHITECTURE.md)
- **Master flight mechanics** → [Flight & Cameras](FLIGHT_AND_CAMERAS.md)
- **Set up multiplayer** → [Multiplayer](MULTIPLAYER.md)
- **Configure EOS** → [EOS Setup](EOS_SETUP.md)
- **Troubleshoot issues** → [Troubleshooting](TROUBLESHOOTING.md)

---

**Ready to fly?** Load the main menu and press Play. Welcome to Aerial Thunder!
