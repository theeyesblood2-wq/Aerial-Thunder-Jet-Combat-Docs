# Troubleshooting Guide

## Getting Help

This guide covers common issues and solutions. If your issue isn't listed, check:
- Relevant system guide (Flight, Weapons, Multiplayer, etc.)
- [Settings Reference](SETTINGS_REFERENCE.md) for configuration issues
- [Quick Start](QUICK_START.md) for basic setup

---

## Installation & Startup Issues

### Project Won't Open

**Symptom:** UE 5.7 won't open the Aerial Thunder project

**Possible Causes & Solutions:**

1. **Visual Studio 2022 not installed**
   - Download Visual Studio 2022 Community
   - Install C++ development tools
   - Restart UE and project

2. **Missing .NET Framework**
   - Install .NET Framework 4.7.2 or higher
   - Restart Windows
   - Retry opening project

3. **Corrupted intermediate files**
   - Delete `Intermediate/` and `Binaries/` folders
   - Delete `Saved/` folder (optional; saves player data)
   - Reopen project
   - Recompile C++ modules

4. **Wrong Unreal Engine version**
   - Verify project uses UE 5.7
   - Upgrade UE if using older version
   - Regenerate Visual Studio project files

### Compilation Errors

**Symptom:** Project fails to compile with C++ errors

**Solutions:**

1. **Clean rebuild**
   ```
   Delete: Intermediate/, Binaries/, Saved/
   Reopen project in UE
   ```

2. **Update Visual Studio**
   - Install latest Visual Studio 2022 updates
   - Install latest C++ tools
   - Restart UE

3. **Verify plugin dependencies**
   - Edit → Plugins
   - Search "Aerial" or "Jet"
   - Both plugins should be enabled
   - Restart editor if disabled any

4. **Check compile errors in Output Log**
   - Window → Output Log
   - Search for `error` (not warning)
   - Fix reported issues
   - Recompile

### Game Crashes on Launch

**Symptom:** Game starts then immediately crashes

**Solutions:**

1. **Delete Saved data**
   ```
   Navigate to Project/Saved/
   Delete entire Saved/ folder
   Restart project
   ```

2. **Verify map loads**
   - Content Browser → Show Plugin Content
   - AT_GM Content → Maps → MainMenu
   - Double-click MainMenu to load
   - If it loads, map is OK

3. **Check system requirements**
   - Windows 10 or 11 (64-bit)
   - 16 GB RAM minimum
   - GPU with 6 GB VRAM
   - DirectX 12 compatible

4. **Review crash logs**
   - Logs stored in `Project/Saved/Logs/`
   - Most recent .log file
   - Search for "fatal error"
   - Note the error and research

---

## Flight & Control Issues

### Controls Don't Respond

**Symptom:** Keyboard/mouse input not controlling aircraft

**Solutions:**

1. **Ensure game window has focus**
   - Click in game window
   - Verify window is active (title bar not greyed out)

2. **Check pause state**
   - Press Escape or P
   - Verify "PAUSED" message appears/disappears
   - Resume game if paused

3. **Verify input bindings**
   - Settings → Controls
   - Check default keys are mapped
   - Test a key (e.g., press W)
   - Should see aircraft pitch up in-game

4. **Try gamepad if keyboard fails**
   - Connect gamepad
   - Restart game
   - Test controller input

5. **Restart input system**
   - Alt-Tab away from game
   - Alt-Tab back to game
   - Try controls again

### Aircraft Spins Out of Control

**Symptom:** Aircraft rotates wildly and crashes

**Causes & Solutions:**

1. **Over-input on controls** — Reduce sensitivity
   - Settings → Controls → Mouse Sensitivity
   - Decrease from 1.0 to 0.7
   - Try again with gentler inputs

2. **Stall condition** (Advanced mode)
   - Lower nose (press S)
   - Increase throttle (press Shift)
   - Wait for speed to recover
   - Gradually level wings

3. **Inverted controls**
   - Settings → Controls → Invert Pitch
   - Toggle off (should be Off by default)
   - Retry

4. **Wrong flight mode**
   - Settings → Gameplay → Flight Mode
   - Select Arcade mode if in Advanced
   - Arcade is more forgiving

### Can't Take Off

**Symptom:** Aircraft won't lift off the ground despite nose-up

**Solutions:**

1. **Insufficient runway**
   - Need at least 3,000 feet of clear runway
   - Try open area instead
   - Free Flight mode if testing

2. **Throttle not at full**
   - Hold Shift to increase throttle
   - Verify throttle gauge reaches ~80-90%
   - Gradually increase; don't jerk it

3. **Incorrect pitch angle**
   - In Arcade mode: Pitch up when ~80 knots
   - In Advanced mode: Rotate at ~80 knots; liftoff at ~100 knots
   - Don't pitch too aggressively

4. **Weight/fuel too high**
   - Try with reduced loadout (fewer weapons)
   - Land and refuel to see if fuel affects takeoff
   - Default loadout should work

### Landing Too Hard / Crashes

**Symptom:** Aircraft crashes on landing or takes excessive damage

**Solutions:**

1. **Too steep descent**
   - Aim for 5-10 degree descent angle
   - Use air brake (Space) to shallow descent
   - Approach should feel shallow

2. **Too fast on approach**
   - Reduce speed earlier
   - Use air brake in descent
   - Approach speed should be 120-140 knots

3. **Not deploying landing gear**
   - Press G before landing
   - Verify landing gear indicator shows down
   - Smooth landing with gear down

4. **Landing on wrong surface**
   - Try landing on runways only
   - Grass/water/mountains = crash
   - Use autopilot for smooth descent if available

5. **Practice landing**
   - Free Flight mode
   - Pick flat area
   - Practice approach and flare
   - Build landing skills gradually

### Stalling Repeatedly (Advanced Mode)

**Symptom:** Aircraft keeps stalling and falling from sky

**Solutions:**

1. **Monitor airspeed constantly**
   - Watch right side of HUD (airspeed tape)
   - Red region = stall zone
   - Keep speed above stall speed line

2. **Reduce pitch aggressively**
   - Don't pitch up more than 45 degrees
   - Reduce pitch when airspeed bleeds
   - Pitch to climb, not roll to climb

3. **Climb gradually**
   - Don't climb at more than 20 degree angle
   - Trade airspeed for altitude slowly
   - Maintain minimum safe airspeed

4. **Use auto-level frequently**
   - Press H to engage auto-level
   - Helps recover from excessive pitch
   - Reduces stall risk significantly

5. **Switch to Arcade mode**
   - Advanced stalls are punishing
   - Learn in Arcade first
   - Graduate to Advanced when comfortable

### Camera Feels Jerky / Shaky

**Symptom:** Camera movement is stuttering or not smooth

**Solutions:**

1. **Reduce mouse sensitivity**
   - Settings → Controls → Mouse Sensitivity
   - Lower to 0.7-0.8
   - Slower movement = smoother feel

2. **Check frame rate**
   - Should be 60 FPS minimum; 90+ better
   - Monitor in top-left corner (if FPS display enabled)
   - If low FPS, lower graphics settings

3. **Try different camera mode**
   - Press V to cycle cameras
   - Chase camera (far back) usually smoothest
   - Cockpit camera most jarring due to limited view

4. **Disable motion blur**
   - Settings → Graphics → Motion Blur
   - Set to 0
   - Can cause perceived shakiness

5. **Restart game**
   - Close and reopen application
   - Often fixes temporary jitter

---

## Weapons & Combat Issues

### Gun Seems Inaccurate

**Symptom:** Gun rounds miss distant targets consistently

**Solutions:**

1. **You're too far away**
   - Get closer (within 1 km)
   - Gun is short-range weapon
   - Move closer for reliable hits

2. **You're not leading target**
   - In Advanced mode, lead target motion
   - Aim ahead of where target is
   - Requires practice and timing

3. **Too much speed**
   - Slow down to improve accuracy
   - Fast passes overshoot
   - Match target speed for accuracy

4. **Aim assist disabled**
   - Settings → Gameplay → Aim Assist
   - Turn On (if it's Off)
   - Helps with lead calculation

5. **Practice aiming**
   - Use training mission
   - Practice against stationary targets
   - Build muscle memory for leading

### Missiles Won't Lock

**Symptom:** Can't get lock-on despite trying

**Solutions:**

1. **Target out of range**
   - Missile range is ~20 km
   - Get closer to target
   - HUD shows range to target

2. **No line of sight**
   - Terrain blocking radar
   - Climb to higher altitude
   - Maneuver to get LOS

3. **Wrong radar mode**
   - Settings → Gameplay → Radar Mode
   - Try different mode (Pulse/Doppler/TWS)
   - Some modes better for locking

4. **Target too slow**
   - Stationary targets need Pulse mode
   - Doppler mode filters stationary targets
   - Switch modes if having trouble

5. **Radar interference**
   - Terrain can block radar
   - Maneuver behind target
   - Get closer for more certain lock

### Flares Don't Stop Missiles

**Symptom:** Deploy flares but missile still hits

**Solutions:**

1. **Deploy too late**
   - Deploy as soon as missile warning sounds
   - Don't wait for missile to get close
   - Early deployment better than late

2. **Not maneuvering**
   - Deploy flares AND maneuver hard
   - Hard turn while deploying
   - Combination stops missile

3. **Multiple missiles**
   - Single salvo may not stop multiple missiles
   - Deploy multiple flare patterns
   - Maneuver aggressively between deployments

4. **Out of flares**
   - Check flare count on HUD
   - If at 0, no flares available
   - Refuel/rearm at base

5. **Wrong difficulty**
   - Advanced/Ace AI fires guided missiles
   - Harder to evade than Normal AI
   - Practice against Normal first

---

## Multiplayer Issues

### Can't Connect to Server

**Symptom:** "Connection failed" when trying to join server

**Solutions:**

1. **Wrong IP address**
   - Verify server IP is correct
   - Ask host for correct IP
   - Format: 192.168.X.X:7777

2. **Server not running**
   - Verify host has started server
   - Server should show in LAN browser
   - Ask host to restart server

3. **Firewall blocking connection**
   - Windows Firewall may block game
   - Go to Windows Firewall settings
   - Allow Aerial Thunder through firewall
   - Restart game

4. **Incorrect port**
   - Default port is 7777
   - If custom port, verify it matches
   - Ask host for correct port

5. **Network timeout**
   - Try again (may be temporary)
   - Check internet connection
   - Try different server if available

### Lag / High Latency

**Symptom:** Other players teleporting; gameplay feels delayed

**Solutions:**

1. **Check internet speed**
   - Minimum: 5 Mbps download / 2 Mbps upload
   - Test at speedtest.net
   - Upgrade ISP if too slow

2. **Close other applications**
   - Video streaming uses bandwidth
   - Large downloads interfere
   - Close unnecessary apps

3. **Move closer to router**
   - WiFi connection weaker at distance
   - Move device closer to router
   - Wired connection better than WiFi

4. **Change servers**
   - Try different server
   - Some servers farther than others
   - Regional servers usually better

5. **Check ping**
   - Settings → Multiplayer → Show Ping
   - Display ping on HUD
   - Below 100 ms ideal; 200+ problematic

### Disconnected from Game

**Symptom:** Kicked out of multiplayer match unexpectedly

**Solutions:**

1. **Network interruption**
   - Check internet connection
   - Restart router if needed
   - Rejoin game if still active

2. **AFK (Away from Keyboard) timeout**
   - Idle too long without input
   - Game kicks inactive players
   - Stay active to remain connected

3. **Kicked for poor connection**
   - Ping too high
   - Packet loss too high
   - Connect from better network

4. **Server crashed**
   - Host may have shut down server
   - Ask host to restart
   - Try different server

5. **EOS authentication failed**
   - EOS session expired
   - Log out and back in
   - Restart application

---

## Graphics & Performance Issues

### Game Running Slowly (Low FPS)

**Symptom:** Game feels choppy; frame rate below 60 FPS

**Solutions:**

1. **Lower graphics settings**
   - Settings → Graphics → Quality
   - Select "Low" preset
   - Can increase if performance improves

2. **Lower resolution**
   - Settings → Graphics → Resolution
   - Try 1920×1080 instead of higher
   - Major FPS improvement

3. **Disable expensive features**
   - Motion Blur → 0
   - Ray Tracing → Off
   - Reflections → Off
   - Bloom → Off

4. **Close background applications**
   - Task Manager → See CPU/GPU usage
   - Close Chrome, Discord, etc.
   - Free up system resources

5. **Update graphics drivers**
   - NVIDIA/AMD driver update
   - Often includes performance improvements
   - Restart after update

### Graphical Artifacts / Visual Glitches

**Symptom:** Flickering, visual glitches, or rendering errors

**Solutions:**

1. **Update graphics drivers**
   - Outdated drivers cause glitches
   - Visit NVIDIA/AMD website
   - Download latest driver
   - Restart after install

2. **Disable DLSS (if enabled)**
   - Can cause visual artifacts
   - Settings → Graphics → DLSS
   - Disable or set to off

3. **Verify graphics hardware**
   - GPU may be overheating
   - Check GPU temperature
   - May need to replace thermal paste

4. **Reinstall graphics drivers**
   - Complete uninstall (not just update)
   - Restart
   - Reinstall latest version

5. **Lower graphics quality**
   - Graphics settings → Low
   - Some GPUs have compatibility issues
   - Try lower quality presets

---

## Audio Issues

### No Sound

**Symptom:** Game produces no audio output

**Solutions:**

1. **Check master volume**
   - Settings → Audio → Master Volume
   - Should be > 0%
   - Increase if too low

2. **Check OS audio settings**
   - Windows Sound settings
   - Verify output device not muted
   - Check volume level

3. **Verify audio device connected**
   - Speakers/headphones plugged in
   - Device shows in Windows audio settings
   - Try different audio device

4. **Restart audio engine**
   - Alt-Tab away from game
   - Alt-Tab back
   - Audio should work

### Audio Cutting Out / Crackling

**Symptom:** Audio drops, crackling, or distortion

**Solutions:**

1. **Reduce audio quality**
   - Settings → Audio → Audio Quality
   - Lower setting reduces CPU load
   - May improve crackling

2. **Update audio drivers**
   - Device Manager → Sound devices
   - Right-click → Update driver
   - Restart after update

3. **Disable audio enhancements**
   - Windows audio settings
   - Disable enhancements for device
   - Can cause crackling

4. **Close audio-heavy applications**
   - Discord, Spotify
   - Voice chat uses audio resources
   - Close to improve game audio

---

## Save/Progression Issues

### Progress Not Saving

**Symptom:** Mission completion not saved; progression lost

**Solutions:**

1. **Check autosave**
   - Autosave happens between levels
   - Verify you completed mission fully
   - Check results screen

2. **Cloud save conflict**
   - May not have synced yet
   - Wait 30 seconds after mission complete
   - Restart game to verify save

3. **Disk space issue**
   - Check free disk space
   - Need at least 10 GB free
   - Delete old files if needed

4. **Permissions issue**
   - Check folder permissions
   - Saved/ folder may be read-only
   - Change permissions in properties

### Can't Load Save File

**Symptom:** "Load failed" when trying to load mission save

**Solutions:**

1. **Save file corrupted**
   - Delete save file: Saved/SaveGames/
   - Start mission fresh
   - Re-complete mission

2. **Incompatible version**
   - If game updated, old saves may break
   - This is rare but possible
   - Start fresh or downgrade

3. **File permissions**
   - Saved/ folder is read-only
   - Right-click → Properties → Uncheck "Read-only"
   - Retry loading

---

## EOS / Online Issues

### EOS Login Fails

**Symptom:** "Authentication failed" when logging in

**Solutions:**

1. **Wrong credentials**
   - Verify Epic Games username/password
   - Account at epicgames.com
   - Try reset password if unsure

2. **Network connectivity**
   - Verify internet connection
   - Ping google.com in command prompt
   - Check firewall not blocking connection

3. **EOS misconfiguration**
   - See [EOS Setup](EOS_SETUP.md)
   - Verify credentials in project settings
   - May need to reconfigure

4. **EOS server down**
   - Epic Games servers may be offline
   - Check Epic Games status page
   - Try again later

### Progress Not Syncing

**Symptom:** Cloud progression not saving/loading

**Solutions:**

1. **Cloud save disabled**
   - Settings → Multiplayer → Cloud Sync
   - Ensure enabled
   - Restart game

2. **EOS disconnected**
   - Log out → Log back in
   - Restart application
   - Verify internet connection

3. **Storage quota exceeded**
   - Cloud storage has limits
   - Delete old saves
   - Reduce save file size

---

## Report a Bug

### How to Report

1. **Gather information**
   - Reproduce the bug consistently
   - Note exact steps to reproduce
   - Screenshot or video if possible
   - Check game version

2. **Check existing reports**
   - Search GitHub Issues
   - Your bug may already be reported
   - Add +1 to existing report

3. **Create detailed report**
   - Title: Clear description
   - Steps to reproduce: Exact steps
   - Expected result: What should happen
   - Actual result: What actually happens
   - System info: OS, GPU, CPU, RAM

4. **Attach files**
   - Screenshot of issue
   - Video of bug (if helpful)
   - Log file: Saved/Logs/

---

## Performance Troubleshooting Flowchart

```
Game Running Slow?
├─ Check FPS: Settings → Show FPS
├─ If 20-40 FPS:
│  └─ Lower graphics: Settings → Graphics → Low
├─ If 40-60 FPS:
│  └─ Close background apps
├─ If still slow:
│  └─ Update graphics drivers
└─ If no improvement:
   └─ Check system requirements (may be insufficient)
```

---

## Support Resources

- **Documentation:** Full guides for all systems
- **Quick Start:** [Quick Start Guide](QUICK_START.md)
- **Settings:** [Settings Reference](SETTINGS_REFERENCE.md)
- **EOS:** [EOS Setup](EOS_SETUP.md)
- **GitHub Issues:** Report bugs on repository

---

**Face the issue. Find the solution. Get back to flying.**
