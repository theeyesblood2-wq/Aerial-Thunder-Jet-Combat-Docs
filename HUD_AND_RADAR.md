# HUD & Radar Guide

## Cockpit HUD Overview

The Heads-Up Display (HUD) is the primary interface for flight operations. All critical information is rendered directly in the cockpit view, allowing pilots to maintain focus on the horizon.

---

## HUD Elements

### Flight Instruments

#### Altitude Tape (Left Side)
- **Display:** Vertical scale showing altitude above ground
- **Units:** Feet
- **Color coding:**
  - Green: Safe altitude
  - Yellow: Caution zone (low altitude)
  - Red: Danger (ground collision risk)
- **Update rate:** Real-time

#### Airspeed Tape (Right Side)
- **Display:** Vertical scale showing true airspeed
- **Units:** Knots
- **Stall warning:** Red chevron indicates stall speed
- **Max safe speed:** Red line at aircraft maximum
- **Color zones:**
  - Green: Safe operating range
  - Yellow: Caution zone
  - Red: Overspeed/Stall danger

#### Attitude Indicator (Center)
- **Display:** Artificial horizon showing aircraft pitch and roll
- **Wings:** Small aircraft icon with roll bars
- **Horizon line:** Shows true horizon
- **Bank angle:** Displayed numerically or via lines
- **Pitch:** Green arc = level; up/down = climb/descent

#### Heading Indicator (Top Center)
- **Display:** Compass showing cardinal directions (N, S, E, W)
- **Heading:** Numerical value (0-360 degrees)
- **Track:** Shows current direction of travel
- **Course:** Shows desired heading if engaged in autopilot

### Engine Instruments

#### Throttle Indicator
- **Display:** Shows current throttle position (0-100%)
- **Reference:** Helps verify throttle input is being applied
- **Target indication:** May show throttle input vs. actual spool

#### Engine Temperature Gauge (Advanced Mode)
- **Display:** Current engine temperature as percentage
- **Normal range:** 40-80%
- **Caution zone:** 80-100%
- **Critical:** 100%+ (engine damage begins)

#### Fuel Gauge
- **Display:** Remaining fuel as percentage
- **Warnings:**
  - 30%: Caution flag displayed
  - 20%: Recurring audio warning ("Fuel low")
  - 10%: Continuous warning ("Fuel critical")
  - 0%: Engine stalls; must land immediately

### Weapon Systems

#### Weapons Display (Lower Left)
- **Gun ammo:** Unlimited (or shows round count if limited)
- **Rockets:** Count remaining (e.g., "RCT 8/16")
- **Missiles:** Count remaining (e.g., "MSL 4/8")
- **Flares:** Count remaining (e.g., "FLR 32/64")
- **Selected weapon:** Highlighted/underlined

#### Gun Pipper (Center)
- **Display:** Circular reticle (gun cross)
- **Color:** Red when ready; changes when overheating
- **Function:** Point where gun rounds will impact
- **Range:** Converges at ~500 meters

#### Missile Tone Indicator
- **Status display:** Shows missile target lock status
- **Colors:**
  - White: Searching
  - Yellow: Locking (building lock)
  - Green: Locked and ready to fire
  - Red: Lost lock / missile in flight
- **Audio:** Tone changes with status

### Targeting Information

#### Target Box (Center/Upper)
When a target is locked or in acquisition:
- **Call sign:** Enemy/ground unit identifier
- **Range:** Distance in kilometers
- **Bearing:** Compass heading to target
- **Altitude:** Target altitude above ground
- **Speed:** Target airspeed in knots

#### Threat Warning
- **Color coding:** Threat level indicated by box color
  - Green: Low threat
  - Yellow: Medium threat
  - Red: High/active threat
- **Audio cue:** Warning tone plays for high threats

### Navigation & Waypoints

#### Objective Display
- **Current objective:** Listed at top of screen
- **Waypoint marker:** Shows next navigation point
- **Distance to waypoint:** Displayed in kilometers
- **Bearing to waypoint:** Compass direction

#### Mission Timer
- **Elapsed time:** Time in mission
- **Time remaining:** Mission timeout (if applicable)
- **Warning:** Flashes when approaching timeout

---

## Radar System

### Radar Modes

#### Pulse Search Mode
- **Range:** 20 km radius
- **Update rate:** Slower (2-3 Hz)
- **Coverage:** Hemisphere ahead of aircraft
- **Best for:** Long-range target acquisition
- **Blind spots:** Directly behind aircraft; terrain-masked areas

#### Pulse Doppler Mode
- **Range:** 15 km radius
- **Update rate:** Medium (3-4 Hz)
- **Advantage:** Filters stationary targets (clutter rejection)
- **Best for:** Detecting moving aircraft
- **Limitation:** May miss low-altitude or slow targets

#### Track While Scan (TWS)
- **Range:** 10 km
- **Tracks:** Multiple targets simultaneously
- **Update rate:** Fast (5-10 Hz)
- **Best for:** Multiplayer dogfights with multiple enemies
- **Limitation:** Higher power consumption

### Radar Display

#### Radar Scope (Lower Left Corner)
- **Format:** Circular scope with range rings
- **Range rings:** Show distance (0, 5, 10, 15, 20 km)
- **North up:** Display is always oriented with north at top
- **Own aircraft:** Center dot or symbol

#### Target Symbology

| Symbol | Meaning |
|--------|---------|
| **Green circle** | Friendly aircraft |
| **Red square** | Enemy aircraft |
| **Blue triangle** | Ground target (friendly) |
| **Red X** | Enemy ground target |
| **Yellow + sign** | Unidentified contact |
| **Track line** | Target motion vector |

#### Radar Contacts
Each radar contact displays:
- **Position:** Relative bearing and range
- **Altitude:** Small number indicating flight level
- **Speed:** Vector line shows direction and rate of motion
- **Track number:** Numeric identifier for correlation

### Radar Targeting

#### Lock-On Sequence
1. **Radar mode selected** — Choose appropriate mode
2. **Scan area** — Radar sweeps designated area
3. **Contact acquired** — Target appears on scope
4. **Single target mode** — Isolate one target
5. **Lock sequence begins** — Audio tone changes
6. **Lock established** — Target box turns green
7. **Missile ready** — Fire light illuminates

#### Lock Time
- **Stationary target:** 1-2 seconds
- **Maneuvering target:** 2-4 seconds
- **Evasive maneuvering:** 3-5+ seconds

#### Breaking Lock
Enemy can break your lock by:
- Flying behind terrain/mountains
- Rapid altitude changes
- Sharp maneuvers that exceed radar tracking rate
- Deploying chaff/countermeasures

---

## Warning Systems

### Audio Warnings

#### Lock Warning Tone
- **Continuous high-pitched tone:** Another aircraft has locked onto you
- **Action:** Immediately deploy flares and maneuver hard
- **Priority:** Critical; respond immediately

#### Missile Launch Warning
- **Distinctive whooping tone:** Missile has been launched at you
- **Action:** Deploy flares, hard maneuvers, take evasive action
- **Priority:** Highest; immediate threat

#### Proximity Warning
- **Intermittent chirp/beep:** Ground collision imminent or extremely close
- **Action:** Pull up immediately or discontinue landing approach
- **Priority:** Critical; can mean instant crash

#### Engine Overheat Warning
- **Beeping tone:** Engine temperature exceeding safe limits (Advanced mode)
- **Action:** Reduce throttle, cruise at lower settings
- **Priority:** High; can damage engine

#### Fuel Low Warning
- **Recurring warning tone:** Fuel level below 20%
- **Action:** Plan landing immediately
- **Priority:** High; can mean forced landing

#### Fuel Critical Warning
- **Continuous warning tone:** Fuel level below 10%
- **Action:** Land immediately or glide to nearest airfield
- **Priority:** Critical; engine will stall soon

### Visual Warnings

#### Stall Warning Indicator
- **Display:** Flashing red border on attitude indicator
- **Condition:** Airspeed dropping below stall speed
- **Action:** Lower nose, increase throttle to recover
- **Recovery time:** 5-10 seconds in Advanced mode

#### Overspeed Warning
- **Display:** Red border on airspeed tape
- **Condition:** Airspeed exceeding safe limits
- **Action:** Reduce throttle, use air brake
- **Consequence:** Structural damage begins at extreme overspeed

#### Low Altitude Warning
- **Display:** Flashing red altitude tape
- **Condition:** Below 500 feet AGL (Above Ground Level)
- **Action:** Climb or prepare for landing
- **Consequence:** Ground collision risk

#### G-Force Indicator (Advanced Mode)
- **Display:** Numerical G value
- **Greyout zone:** 6-9 G (vision greys out)
- **Blackout zone:** 9+ G (complete loss of vision; aircraft uncontrollable)
- **Recovery:** Reduce bank angle and pitch inputs

---

## Tactical Air Display (TAD)

### TAD Overview
The Tactical Air Display is an advanced situational awareness tool combining:
- Radar data
- Navigation information
- Threat indicators
- Weapon status
- Team positions (multiplayer)

### TAD Layout

#### Main Display Area
- **Central crosshair:** Own aircraft position
- **Map background:** Terrain and waypoint markers
- **Radar overlay:** Friendly/enemy positions
- **Threat annotations:** Active threats highlighted

#### Information Panels

**Left Panel:**
- Current heading
- Altitude
- Airspeed
- Target information

**Right Panel:**
- Weapon status
- Fuel remaining
- Engine parameters
- Time information

**Bottom Panel:**
- Active threats
- Friendly positions
- Mission objectives

---

## HUD Customization

### HUD Opacity
- **Settings → HUD → Opacity**
- Adjust transparency of HUD elements (0-100%)
- Useful for visibility in bright/dark areas

### HUD Scale
- **Settings → HUD → Scale**
- Increase/decrease HUD element size
- Helpful for visibility at different screen resolutions

### HUD Elements Toggle
- **Settings → HUD → Visible Elements**
- Show/hide individual HUD elements
- Customize display for preferred information
- Can enable "Minimal HUD" for immersion

### HUD Color Scheme
- **Settings → HUD → Color Scheme**
- Standard (green)
- Alternative (amber)
- Custom (user-defined)

---

## Reading the Radar Effectively

### Radar Interpretation Tips

1. **Relative bearing:** Contacts move around scope as you turn
2. **Track vector:** Line pointing from contact shows motion direction
3. **Closure rate:** Long vector = fast target; short vector = slow
4. **Altitude:** Small number next to symbol shows altitude blocks (multiply by 1,000 feet)
5. **Range:** Position on scope relative to range rings indicates distance

### Common Radar Contacts

| Contact Type | Radar Symbol | Interpretation |
|--------------|--------------|-----------------|
| Enemy fighter | Red square | Treat as hostile |
| Friendly fighter | Green circle | Don't engage; coordinate |
| SAM site | Red X | Dangerous; avoid |
| Airfield | Red square cluster | High defense area |
| Unidentified | Yellow + | Declare hostile if location hostile |

### Multi-Target Scenarios

When multiple contacts are present:
1. **Identify threat level** — Which targets pose greatest threat?
2. **Assess ranges** — How far away is each target?
3. **Evaluate converging threats** — Are enemies supporting each other?
4. **Prioritize targets** — Which to engage first?
5. **Separate conflicts** — Can you isolate one enemy from others?

---

## Radar & Weapons Integration

### Radar Lock to Missile Fire
1. **Radar contact** — Target appears on scope
2. **Target selection** — Lock radar onto specific target
3. **Build lock** — Audio tone transitions from search to lock
4. **Missile ready** — HUD displays "LOCK" or missile count
5. **Fire missile** — Press missile fire key
6. **Missile guidance** — Radar maintains track until impact or evasion

### Multi-Missile Employment
- **Fire sequence:** First missile departs and seeks target
- **Immediate relock:** Establish lock on same target for second missile
- **Saturation attack:** Fire 2-3 missiles quickly
- **Probability:** Multiple missiles dramatically increase hit probability

### Simultaneous Multiple Targets
In Track While Scan mode:
- **Lock target 1** → Fire missile
- **Lock target 2** → Fire missile
- **Lock target 3** → Fire missile
- Each missile maintains independent track

---

## Troubleshooting HUD & Radar

### Radar Won't Acquire Lock
**Cause:** Target out of radar range or in radar shadow
**Solution:**
1. Move closer to target
2. Climb to higher altitude for better radar coverage
3. Switch radar modes
4. Try visual targeting instead

### HUD Elements Overlapping or Unclear
**Cause:** HUD scale too large or opacity too high
**Solution:**
1. Reduce HUD scale in settings
2. Adjust HUD opacity
3. Try minimal HUD mode
4. Change HUD color scheme

### Radar Contacts Disappearing
**Cause:** Radar clutter, enemy using countermeasures, or target maneuvering
**Solution:**
1. Switch to Pulse Doppler to reject clutter
2. Use TWS mode for better tracking
3. Climb to higher altitude for cleaner radar picture
4. Maneuver to maintain line of sight

### Audio Warnings Too Loud
**Cause:** Master volume or warning volume too high
**Solution:**
1. Settings → Audio → Warning Volume
2. Adjust to comfortable level
3. Don't disable completely (safety feature)

---

## HUD Tips & Tricks

1. **Always check six** — Glance at radar frequently for threats from behind
2. **Trust your HUD** — It's designed for quick reference; learn to read it
3. **Correlate HUD and radar** — Visual contacts should match radar positions
4. **Audio first** — Listen to warnings; react before checking display
5. **Minimal HUD for immersion** — Turn off HUD for maximum realism
6. **TAD for situational awareness** — Check TAD in multiplayer for team positioning
7. **Radar modes matter** — Use Doppler mode in clutter; Search mode for long range
8. **Lock tone is your friend** — Audio lock indication is often faster than visual check
9. **Threat assessment** — Red contacts = hostile; prioritize accordingly
10. **Practice reading radar** — Spend time learning radar symbol positions

---

## Next Steps

- **Learn weapons:** [Weapons & Targeting](WEAPONS_AND_TARGETING.md)
- **Master flight:** [Flight & Cameras](FLIGHT_AND_CAMERAS.md)
- **Challenge AI:** [AI System](AI_SYSTEM.md)

---

**Eyes up. Radar up. Situational awareness is survival.**
