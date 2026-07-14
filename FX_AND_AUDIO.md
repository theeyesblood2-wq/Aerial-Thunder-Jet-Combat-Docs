# FX & Audio Guide

## Audio System Overview

Aerial Thunder features a dynamic audio system with:
- Jet engine sounds with speed-responsive audio
- Radio communications and warnings
- Environmental ambience and weather effects
- Music system that adapts to gameplay intensity
- 3D positional audio for immersive localization

---

## Engine Audio

### Engine Sound Design

#### Flight Envelope Audio
- **Idle** — Quiet turbine hum (landing/taxiing)
- **Cruise** — Steady jet sound (~350 knots)
- **Military Power** — Increased turbine sound
- **Afterburner** — High-intensity roar (if applicable)

#### Speed-Responsive Audio
Engine sound pitch and intensity change based on:
- **Current throttle** — RPM affects frequency
- **Airspeed** — Wind noise increases with speed
- **Altitude** — Less oxygen at altitude affects sound
- **G-forces** — Strain on engine during maneuvers

#### Temperature Effects
- **Cold start** — Engine spool-up sounds (5-10 seconds)
- **Normal operation** — Steady turbine sound
- **Overheating** — High-frequency whine when hot
- **Shutdown** — Spool-down noise (engine winding down)

### 3D Engine Audio Positioning

- **Mono in cockpit** — Equal in both ears from cockpit center
- **Stereo in external view** — Positioned around aircraft
- **Directional** — Comes from engine location (rear of aircraft)
- **Distance fading** — Louder when close, fades with distance

---

## Weapon Audio

### Gun Sound

- **Fire tone** — Distinctive cannon report
- **Tracer impact** — Whip/crack sound at bullet impact
- **Shell casings** — Metallic pinging (cockpit view)
- **Overheat** — Whine as gun gets hot

### Rocket Audio

- **Launch** — Explosive whoosh and roar
- **Flight** — Rocket motor sound during flight
- **Impact** — Explosive detonation and rumble
- **Proximity detonation** — Secondary explosion if near target

### Missile Audio

- **Launch** — Distinctive whoosh; more intense than rockets
- **Flight** — Missile motor sound, diminishing with distance
- **Impact** — Powerful explosion sound
- **Lock tone** — Audio signal during target lock/missile tracking

### Flare Audio

- **Deploy** — Pop/snap as countermeasures dispense
- **Success** — Different tone if missile detonates on flares
- **Warning** — Audio alert when flares running low

---

## Radio Communications

### Mission Radio

#### Briefing & Callouts
- **Commander** — Provides mission briefing
- **Wingmate** — Tactical callouts during flight
- **Controller** — Mission updates and warnings
- **Frequency changes** — Realistic radio switching

### Radio Tones

| Tone | Meaning | Response |
|------|---------|----------|
| **Chirp (search)** | Radar searching for targets | No immediate action |
| **Steady tone (lock)** | Enemy locked onto you | Deploy flares & maneuver |
| **Whooping (threat)** | Missile launched at you | Emergency evasion |
| **Beep pattern** | Proximity warning | Pull up or break |
| **Continuous alert** | Critical system failure | Take corrective action |

### Realistic Radio Protocol

- **Callsigns** — Players use assigned callsigns
- **Brevity codes** — Military abbreviations (Tally = visual contact)
- **Frequency discipline** — Realistic radio traffic
- **Squelch tone** — Realistic radio static between transmissions

---

## Warning Systems

### Audio Warnings

#### Altitude Warning
- **Trigger:** Below 500 feet AGL
- **Sound:** Intermittent beep/chirp
- **Response:** Climb or prepare for landing

#### Proximity Warning
- **Trigger:** Terrain collision imminent
- **Sound:** Continuous loud beeping
- **Response:** Immediate pull-up; critical!

#### Stall Warning
- **Trigger:** Airspeed dropping below stall speed (Advanced mode)
- **Sound:** Repetitive buzzer or horn
- **Response:** Lower nose, increase throttle

#### Engine Overheat Warning
- **Trigger:** Engine temperature exceeding safe limits
- **Sound:** High-frequency whining
- **Response:** Reduce throttle

#### Fuel Low Warning
- **Trigger:** Fuel below 20%
- **Sound:** Recurring warning tone every 10 seconds
- **Response:** Plan landing

#### Fuel Critical Warning
- **Trigger:** Fuel below 10%
- **Sound:** Continuous warning tone
- **Response:** Land immediately

#### Lock Warning Tone
- **Trigger:** Enemy radar lock detected
- **Sound:** Medium-pitched continuous tone (changes based on threat level)
- **Response:** Deploy flares and maneuver

#### Missile Launch Warning
- **Trigger:** Missile fired at aircraft
- **Sound:** Rapid whooping/chirping tone
- **Response:** Immediate evasion maneuvers

---

## Environmental Audio

### Weather Effects

#### Rain
- **Effect:** Rain sound on cockpit canopy
- **Intensity:** Varies with rain severity
- **Stops at altitude:** No rain sound above storm clouds
- **Visual correlation:** Matches visual rain FX

#### Thunder
- **Effect:** Distant thunder rumbles
- **Trigger:** During thunderstorm conditions
- **Realism:** Random timing; multiple rumbles possible

#### Wind Noise
- **Effect:** Increases with speed and altitude
- **Pitch:** Higher pitch at higher speeds
- **Cockpit:** Primarily affects cockpit view

### Ambient Audio

#### Airfield Ambience
- **Ground traffic** — Ambient military base sounds
- **Hangars** — Metal clanging, tools
- **Radio chatter** — Distant military communications

#### Ocean Ambience
- **Wave sounds** — Crashing waves if flying low over water
- **Seagulls** — Distant bird calls
- **Wind over water** — Sea breeze effects

#### Urban Ambience
- **City noise** — Traffic and urban sounds
- **Sirens** — Emergency vehicles (if combat over city)
- **Wind through buildings** — Architectural effects

---

## Music System

### Dynamic Music

Music adapts based on gameplay:

#### Calm/Cruise
- **Intensity:** Low-moderate
- **Tempo:** Slow-moderate
- **Mood:** Peaceful, contemplative
- **Trigger:** Level flight, no threats detected

#### Combat Alert
- **Intensity:** Medium-high
- **Tempo:** Moderate-fast
- **Mood:** Tension, action
- **Trigger:** Enemy detected or engaged

#### Dogfight
- **Intensity:** High
- **Tempo:** Fast
- **Mood:** Urgent, intense
- **Trigger:** In active combat engagement

#### Mission Success
- **Intensity:** Moderate
- **Tempo:** Victory pace
- **Mood:** Triumphant
- **Trigger:** Mission objective completed

#### Mission Failure
- **Intensity:** Low
- **Tempo:** Slow
- **Mood:** Defeat
- **Trigger:** Mission failed

### Music Settings

**Settings → Audio → Music:**
- **Music Volume** — 0-100%
- **Dynamic Music** — On/Off (enable adaptive music)
- **Music Intensity** — 0-100% (how intense combat music gets)

---

## Audio Settings & Configuration

### Audio Channels

| Channel | Default | Range | Purpose |
|---------|---------|-------|---------|
| **Master** | 80% | 0-100% | Overall volume |
| **Engine** | 70% | 0-100% | Jet engine sounds |
| **Weapons** | 75% | 0-100% | Gun/rocket/missile sounds |
| **Radio** | 80% | 0-100% | Communications |
| **Warnings** | 90% | 0-100% | Alert tones |
| **Music** | 60% | 0-100% | Background music |
| **Ambience** | 50% | 0-100% | Environmental sounds |

### Audio Presets

**Balanced:**
- All channels at moderate levels
- Good for general gameplay

**Immersive:**
- Engine and ambience enhanced
- Warnings slightly reduced
- Music increased
- Realistic military audio emphasis

**Communication:**
- Radio and warnings maximized
- Music and ambience reduced
- Engine slightly quieter
- Best for competitive play

**Custom:**
- User-defined levels per channel

### Audio Hardware

- **Speakers** — Select output device
- **Headphones** — Optimize for headphone playback
- **Surround Sound** — Enable 5.1/7.1 (if supported)
- **Mono Audio** — For accessibility (accessibility settings)

---

## Visual Effects (FX) System

### Exhaust Effects

Exhaust rendering uses multiple methods (selectable):

#### Static Mesh Exhaust
- **Performance:** Very fast
- **Appearance:** Static mesh trails
- **Realism:** Lower
- **Best for:** Lower-end hardware

#### Niagara FX Exhaust
- **Performance:** Medium
- **Appearance:** Particle-based trails
- **Realism:** Medium-high
- **Best for:** Mid-range hardware

#### Combined Exhaust
- **Performance:** Slower
- **Appearance:** Mesh + particles combined
- **Realism:** High
- **Best for:** High-end hardware

**Setting:** Edit → Project Settings → Engine → Jet Combat → Exhaust Type

### Water Interaction

#### Landing Gear Water Spray
- **Trigger:** Flying low over water
- **Effect:** Spray particles from water surface
- **Intensity:** Varies with speed and altitude
- **Visual:** Visible behind aircraft

#### Cockpit Canopy Droplets
- **Trigger:** Flying through rain or near water
- **Effect:** Droplets on canopy glass
- **Wipers:** Can clear droplets during landing
- **Realism:** Adds immersion

#### Wake Trails
- **Effect:** Water disturbance pattern visible behind aircraft
- **Trigger:** Flying low over water
- **Visual:** Enhances low-altitude flying

### Impact Effects

#### Gun Impact Flashes
- **Trigger:** Gun rounds hitting target
- **Effect:** Muzzle flash and impact spark
- **Color:** Yellow/orange based on materials
- **Visibility:** Visible to all players in multiplayer

#### Missile Impact Explosions
- **Trigger:** Missile detonation
- **Effect:** Large explosion with debris
- **Scale:** Larger for direct hits
- **Audio:** Matches visual effect

#### Ground Impact Dust
- **Trigger:** Landing gear contact with ground
- **Effect:** Dust cloud kicked up
- **Intensity:** Depends on landing speed
- **Spread:** Spreads behind aircraft during takeoff

### Environmental Effects

#### Storm/Rain Particles
- **Trigger:** In stormy weather
- **Effect:** Rain/sleet particles visible in air
- **Density:** Intensity varies by weather setting
- **Cockpit view:** Rain on canopy glass

#### Clouds & Sky
- **Cumulus clouds** — Puffy fair-weather clouds
- **Stratus clouds** — Low overcast
- **Fog** — Reduced visibility
- **Lighting:** Changes with time of day

#### Sun/Sky Lighting
- **Time of day:** Affects lighting color and intensity
- **Shadows:** Real-time shadows on terrain and buildings
- **Lens flares:** Optional sun lens flare effect

### Visual Settings for FX

**Settings → Graphics → Effects:**
- **Particle Quality** — Low/Medium/High/Ultra
- **Water Simulation** — On/Off
- **Bloom Effect** — On/Off
- **Motion Blur** — Amount (0-100%)
- **Depth of Field** — On/Off
- **Screen Space Reflections** — On/Off

---

## Audio-Visual Synchronization

### Synchronized Effects

Effects and audio are precisely timed:
- **Weapon fire** — Audio matches muzzle flash
- **Explosions** — Sound matches visual explosion
- **Engine sounds** — Correlate with throttle position
- **Warnings** — Audio and visual HUD feedback simultaneous

### Latency Compensation

Network latency compensated for:
- **Audio cues** — Played slightly ahead of visual
- **Impact sounds** — Timed to visual impact point
- **Dialogue** — Lip-sync with visual animation

---

## Audio Recording & Customization

### Recording Game Audio

Settings → Audio → Recording:
- **Record to file** — Optional audio recording
- **Format:** WAV/OGG
- **Quality:** Lossless or compressed
- **Usage:** Review gameplay, create videos

### Custom Audio Mods

Advanced users can:
- **Replace audio files** — Place custom files in content/audio/
- **Modify audio settings** — Config files for audio properties
- **Create radio callouts** — Custom mission briefings
- **Design custom music** — Replace background music

---

## Audio Troubleshooting

### No Sound

**Cause:** Audio disabled or volume muted
**Solution:**
1. Check Settings → Audio → Master Volume (should be > 0)
2. Verify speakers/headphones connected
3. Check OS audio settings
4. Restart application

### Audio Crackling/Distortion

**Cause:** Audio buffer underrun or driver issue
**Solution:**
1. Reduce audio quality in settings
2. Update audio drivers
3. Lower frame rate
4. Restart application

### One-Sided Audio (Only Left or Right)

**Cause:** Mono mode enabled or audio device issue
**Solution:**
1. Verify stereo is enabled: Settings → Audio → Mono Audio = Off
2. Check speaker/headphone connections
3. Test with different audio output device

### Music Not Changing Dynamically

**Cause:** Dynamic music disabled or music volume too low
**Solution:**
1. Enable dynamic music: Settings → Audio → Dynamic Music = On
2. Increase music volume
3. Verify intensity setting is not at 0%

### Radio Callouts Not Playing

**Cause:** Radio volume too low or dialogue suppressed
**Solution:**
1. Increase radio volume: Settings → Audio → Radio Volume
2. Verify dialogue is not muted
3. Check in-game radio is not disabled
4. Restart mission

---

## Audio Tips

1. **Use headphones** — Better 3D audio positioning
2. **Adjust warning volume** — Keep high for safety
3. **Balance levels** — Don't let one channel overwhelm others
4. **Test surroundsound** — If available, enables immersion
5. **Enable dynamic music** — Enhances engagement
6. **Mute when not gaming** — Reduces distraction
7. **Use audio presets** — Start with preset, customize from there
8. **Monitor audio input** — Ensure mic is muted during gameplay

---

## Next Steps

- **Customize audio:** Settings → Audio
- **Adjust FX:** Settings → Graphics → Effects
- **Start mission:** Single Player → Campaign

---

**Hear the sound. Feel the impact. Experience the immersion.**
