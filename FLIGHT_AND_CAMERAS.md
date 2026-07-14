# Flight & Cameras Guide

## Overview

Aerial Thunder features a complete flight system with two distinct control modes and three camera perspectives. The flight mechanics are designed for both casual arcade gameplay and serious simulation-style flying.

---

## Flight Modes

### Arcade Flight Mode

**Designed for:** Casual players, fast-paced action

#### Characteristics
- Simplified, forgiving flight physics
- Automatic stabilization during turns
- Instant throttle response
- Reduced stall risk
- Easy takeoffs and landings
- Immediate camera response

#### Best For
- Learning the game
- Fast-paced combat missions
- Players unfamiliar with flight mechanics

#### Control Feel
- Direct response to pitch/roll inputs
- Aircraft quickly returns to level flight if input is released
- Generous turning radius; minimal overshoot

---

### Advanced Flight Mode

**Designed for:** Simulation enthusiasts, competitive players

#### Characteristics
- Realistic flight physics
- Momentum-based controls (inputs have inertia)
- Throttle affects speed and climb rate realistically
- Stall mechanics and recovery maneuvers
- Complex takeoff and landing procedures
- Requires skill and situational awareness

#### Best For
- Flight sim fans
- Competitive multiplayer
- Extended campaign missions

#### Control Feel
- Aircraft carries momentum through turns
- Aggressive pitch-up can stall the aircraft (requiring nose-down recovery)
- Throttle changes gradually affect altitude and energy
- Requires planning ahead for maneuvers

#### Stall Recovery
If you stall (indicated by flashing HUD warning and audio alert):
1. Lower the nose (push forward / press S)
2. Increase throttle (press Shift)
3. Wait for airspeed to recover
4. Gradually pull back to level flight

---

## Flight Controls

### Primary Control Axes

| Input | Arcade | Advanced |
|-------|--------|----------|
| **Pitch (W/S)** | Direct nose up/down | Affects pitch rate; builds/bleeds energy |
| **Roll (A/D)** | Direct bank left/right | Aircraft rolls smoothly; holds bank |
| **Yaw (Q/E)** | Direct nose rotation (horizontal) | Affects heading; limited effect without roll |
| **Throttle (Shift/Ctrl)** | Immediate speed change | Gradual speed change; affects climb rate |

### Flight Assistance Systems

#### Auto Level (H Key)
Automatically levels the aircraft wings and pitch:
- Useful for recovery from complex maneuvers
- Engages for ~3 seconds then disengages
- Can be toggled on/off via settings
- Not available in Advanced mode on highest difficulty

#### Air Brake (Space Key - In Flight)
Reduces speed and increases descent rate:
- Used for emergency deceleration
- Useful for tight landing approaches
- Can be held or toggled
- Decreases energy rapidly

#### Ground Brake (Space Key - On Ground)
Applied after landing:
- Slows the aircraft to a stop
- Can only be engaged when wheels are down
- Must be held

---

## Takeoff & Landing

### Takeoff Procedure

#### Arcade Mode (Simple)
1. Press **Enter** to start engines
2. Hold **Shift** to increase throttle to ~60%
3. Press **W** to pitch up slightly
4. Aircraft lifts off automatically when airspeed is sufficient
5. Press **H** for auto-level once airborne

#### Advanced Mode (Realistic)
1. Press **Enter** to start engines (takes ~5 seconds)
2. Gradually increase throttle with **Shift** while maintaining centerline
3. At ~80 knots, gently pull back on pitch (W key) to rotate
4. Aircraft becomes airborne at ~100+ knots
5. Retract landing gear with **G** once safely airborne
6. Continue climbing to safe altitude
7. Level wings and establish cruise

### Landing Procedure

#### Before Landing
1. **Reduce speed:** Use **Ctrl** to reduce throttle; use **Space** for air brake if needed
2. **Deploy landing gear:** Press **G** (lowering gear increases drag and warning sounds)
3. **Enter descent:** Pitch down gently (S key) to lose altitude

#### Final Approach
1. **Aim for runway:** Line up nose with landing surface
2. **Control descent rate:** Adjust pitch to maintain gentle descent (100-200 ft/min)
3. **Maintain airspeed:** ~120-140 knots is ideal (varies by aircraft)
4. **Watch altimeter:** HUD shows altitude above ground

#### Landing
1. **Flare:** Gently pull back (W key) just before touchdown to reduce descent rate
2. **Touchdown:** Gentle contact with ground (excessive descent speed = damage)
3. **Engage ground brake:** Hold **Space** after landing to stop
4. **Cut engines:** Press **Enter** to shut down

#### Landing Tips
- **Smooth is good:** Jerky, hard landings can damage the aircraft
- **Slow and steady:** Approach at minimum controllable speed
- **Use air brake:** Deploy air brake to steepen descent without building speed
- **Watch the HUD:** Altitude, descent rate, and airspeed are critical

---

## Advanced Maneuvers

### Energy Management (Advanced Mode)
Every maneuver trades speed (energy) for altitude or turning performance:
- **Climbing** consumes energy (reduces speed)
- **Diving** builds energy (increases speed)
- **Turning** consumes energy (speed bleeds when banking)
- **Level flight** at throttle stabilizes energy

#### Energy States
- **High energy:** Fast, shallow turns, can climb easily
- **Neutral energy:** Balanced; sustainable turns and climbs
- **Low energy:** Slow, tight turns, difficult to climb; stall risk

### Dogfighting Maneuvers

#### Scissors (Turning Duel)
1. Both aircraft turn toward each other
2. Narrow your turn radius more than opponent
3. Try to gain position behind them
4. If they out-turn you, reverse direction suddenly

#### Vertical Loop
1. Pull up sharply (W key while increasing throttle)
2. Continue pulling through the top
3. Complete the circle and re-engage
4. Excellent for losing a pursuer; requires high energy

#### Split-S (Escape Maneuver)
1. Roll upside down (A or D key while banking)
2. Pull back (W key) to invert and dive
3. Quickly lose altitude and speed
4. Useful for evading missiles or pursuers

#### Immelman (Climb & Roll)
1. Pitch up sharply (W key)
2. At the top of the climb, roll inverted (A or D)
3. Pull through to level flight, now facing opposite direction
4. Advanced maneuver; requires practice

### Energy Bleed Awareness
Turns in Advanced mode consume energy:
- **Tight turns** (aggressive pitch + roll) bleed energy fastest
- **Shallow turns** (gentle inputs) bleed energy slower
- **Descending turns** gain energy
- **Climbing turns** consume extra energy
- **Stalling** occurs when airspeed drops too low

---

## Camera System

### Camera Modes

#### Cockpit View (First-Person)
**Key:** V to cycle; Hold V to stay in cockpit  
**Zoom:** Mouse wheel to adjust field of view

- Immersive, realistic perspective
- Limited visibility (narrow field of view)
- Instrument panel and HUD visible
- Audio is directional from cockpit position
- Most challenging for dogfighting (visibility limited)

#### Shoulder Camera (Third-Person Behind)
**Key:** V to cycle  
**Zoom:** Mouse wheel to adjust distance

- Camera positioned behind the aircraft at ~50 meters
- Can see the entire airframe and surrounding area
- Better situational awareness than cockpit
- Still maintains flight-focused perspective
- Recommended for learning and general gameplay

#### Chase Camera (Distant Third-Person)
**Key:** V to cycle  
**Zoom:** Mouse wheel to adjust distance

- Camera far behind aircraft (~200+ meters)
- Cinematic, wide field of view
- Excellent for complex maneuvers and dogfighting
- Shows full combat arena
- Great for multiplayer and missions

### Camera Controls

| Control | Function |
|---------|----------|
| **Mouse X-Axis** | Look left/right (Yaw) |
| **Mouse Y-Axis** | Look up/down (Pitch) |
| **Mouse Wheel Up** | Zoom in (closer to aircraft) |
| **Mouse Wheel Down** | Zoom out (farther from aircraft) |
| **V Key** | Cycle to next camera mode |
| **5 Key or Middle Mouse** | Reset camera to default zoom/angle |

### Camera Sensitivity

Adjust mouse look sensitivity in **Settings → Controls**:
- **Low sensitivity:** Smoother, easier control; better for precise aiming
- **High sensitivity:** Faster look; requires more precision
- **Default:** Balanced for most players

---

## Throttle Management

### Throttle States

| State | Throttle % | Use Case |
|-------|-----------|----------|
| **Idle** | 0% | Coasting, landing, hovering |
| **Cruise** | 40-60% | Sustained flight, fuel efficiency |
| **Climb** | 70-85% | Gaining altitude, energy |
| **Full Power** | 100% | Acceleration, dogfighting, emergency |

### Throttle Response

#### Arcade Mode
- Throttle responds instantly
- Speed changes immediately
- Easy to manage

#### Advanced Mode
- Throttle changes gradually (takes 3-5 seconds to spool)
- Speed and altitude changes lag behind throttle input
- Requires planning ahead
- Overspeeding causes fuel consumption and engine stress

### Overspeeding
At extreme speeds:
- Aircraft may lose control authority (harder to turn)
- Engine temperature rises
- Fuel consumption increases
- HUD displays warning
- Can cause structural damage if speed limits exceeded

---

## Flight Envelope & Limitations

### Speed Limits

| Parameter | Arcade | Advanced |
|-----------|--------|----------|
| **Minimum Safe Speed** | ~60 knots | ~90 knots (stall speed) |
| **Cruise Speed** | 300-400 knots | 250-350 knots |
| **Max Speed** | 500+ knots | 450+ knots |
| **Maximum Safe** | 550 knots | 500 knots |

### Altitude Limits

| Limit | Value | Effect |
|-------|-------|--------|
| **Minimum** | Ground level | Can crash |
| **Safe minimum** | 500 ft | Below this, landing zone should be nearby |
| **Service ceiling** | 35,000 ft | Maximum designed altitude |
| **Pressure ceiling** | 40,000 ft | Above this, oxygen systems fail |

### G-Force Limits

In Advanced mode, extreme maneuvers apply G-forces:
- **0-3 G:** Normal, sustainable
- **3-6 G:** Uncomfortable but tolerable for short duration
- **6-9 G:** Pilot experiences greyout (vision dims)
- **9+ G:** Pilot blackout; aircraft becomes uncontrollable

Greyout/Blackout Recovery:
1. Reduce bank angle and pitch inputs
2. Level wings
3. Wait for vision to return (2-3 seconds)

---

## Fuel & Engine Management

### Fuel System

#### Fuel Capacity
- **Normal fuel:** Supports ~30 minutes of cruise flight
- **Full throttle:** Consumes fuel in ~15 minutes
- **Idle:** Consumes minimal fuel

#### Fuel Warnings
- HUD shows fuel percentage
- **Fuel low (20%):** Audio warning every 10 seconds
- **Fuel critical (10%):** Continuous warning
- **Empty:** Engine stalls; must land immediately

#### Fuel Recovery
- Fuel only refills on the ground at base/airfield
- Land safely and wait for refuel
- Some missions may provide fuel stations or refuel waypoints

### Engine System

#### Start-Up Sequence
1. Press **Enter** to start
2. Engine spools (5-10 seconds)
3. Instruments come online
4. Ready to taxi

#### Shutdown
1. Reduce throttle to idle
2. Press **Enter** to shut down
3. Engine spools down

#### Engine Overheating (Advanced Mode)
- Prolonged full throttle causes overheating
- HUD displays temperature gauge
- At critical temperature, engine performance reduces
- Solution: Reduce throttle, cruise at idle until cooled

---

## Troubleshooting Flight

### Aircraft Spins Out of Control
**Cause:** Over-input on controls; stall condition
**Solution:**
1. Center the stick (release all control inputs)
2. Push nose down (press S)
3. Increase throttle (press Shift)
4. Once spinning stops, level wings and recover altitude

### Can't Take Off
**Cause:** Insufficient runway or speed
**Solution:**
1. Ensure you have ~3,000 feet of runway minimum
2. Gradually increase throttle; don't jerk it
3. In Arcade mode, pitch up at ~80 knots
4. Wait for wings to become airborne; don't force it

### Landing Crashes Into Ground
**Cause:** Too steep descent or too fast approach
**Solution:**
1. Reduce speed more gradually (use air brake)
2. Maintain shallow descent angle (~5 degrees)
3. Reduce throttle earlier
4. Practice on open landing area first

### Stalling Repeatedly (Advanced Mode)
**Cause:** Pitch too high for current airspeed
**Solution:**
1. Monitor HUD airspeed constantly
2. Reduce pitch input (less aggressive on W key)
3. Maintain minimum airspeed for altitude
4. Use auto-level (H) to help recover

### Camera Feels Jerky
**Cause:** High mouse sensitivity or frame rate issues
**Solution:**
1. Reduce mouse sensitivity in settings
2. Verify frame rate is stable (should be 60+ FPS)
3. Try different camera mode
4. Adjust camera zoom

---

## Flight Settings Reference

Access **Settings → Controls → Flight**:

- **Flight Mode:** Arcade or Advanced
- **Auto Level:** Enabled/Disabled
- **Mouse Sensitivity:** 0.1 to 2.0
- **Throttle Sensitivity:** 0.1 to 2.0
- **Invert Pitch:** Reverse W/S controls
- **Invert Yaw:** Reverse Q/E controls
- **Camera Invert:** Reverse mouse Y-axis
- **Camera Sensitivity:** Separate from flight sensitivity

---

## Tips & Tricks

1. **Practice in Arcade mode first** — Get comfortable with controls before switching to Advanced
2. **Use auto-level frequently** — Press H often to recover from bad attitudes
3. **Always maintain energy** — Monitor speed relative to altitude
4. **Look around often** — Use mouse to look for enemies and navigation markers
5. **Smooth inputs win** — Jerky control inputs cause instability
6. **Fuel management matters** — Plan routes to land before fuel runs out
7. **Landing gear up after takeoff** — Reduces drag and increases speed
8. **Air brake in dogfights** — Tighten your turn radius for hard-to-follow turns
9. **Scissors maneuver** — Often the best way to gain advantage in 1v1 fights
10. **Practice stall recovery** — Essential skill for survival in Advanced mode

---

## Next Steps

- **Learn targeting:** [Weapons & Targeting](WEAPONS_AND_TARGETING.md)
- **Understand the HUD:** [HUD & Radar](HUD_AND_RADAR.md)
- **Master AI combat:** [AI System](AI_SYSTEM.md)
- **Control reference:** [Input & Controls](INPUTS.md)

---

**Take to the skies. Master the flight. Dominate the engagement.**
