# Mission System Guide

## Mission Overview

Aerial Thunder features a complete mission system with campaign progression, dynamic objectives, and extensive customization. The framework supports single-player campaigns, co-op missions, and multiplayer scenarios.

---

## Campaign Structure

### Campaign Organization

```
Aerial Thunder Campaign
├── Mission 1: Infiltration
│   ├── Objective 1: Scout target
│   ├── Objective 2: Mark location
│   └── Objective 3: Extract
├── Mission 2: Defense
│   ├── Objective 1: Intercept bandits
│   ├── Objective 2: Protect convoy
│   └── Objective 3: Consolidate position
└── Mission 3: Strike
    ├── Objective 1: Destroy SAM site
    ├── Objective 2: Raid airfield
    └── Objective 3: Regroup at rally point
```

### Three Complete Campaign Missions

#### Mission 1: Infiltration
**Difficulty:** Easy-Medium  
**Objective:** Scout enemy positions and mark targets

**Primary Objectives:**
1. Navigate to sector alpha
2. Identify and photograph target location
3. Mark three ground targets with radar
4. Return to base safely

**Key Features:**
- Introduction to flight controls and weapons
- Radar/targeting system tutorial
- Multiple waypoints and navigation markers
- Time-based mission (30 minutes)

**Rewards:**
- Mission completion unlocks Mission 2
- Bonus rewards for clean completion (no damage)

#### Mission 2: Defense
**Difficulty:** Medium  
**Objective:** Defend allied assets from air attack

**Primary Objectives:**
1. Intercept first wave of enemy fighters
2. Protect convoy from air attack
3. Hold defensive position against reinforcements
4. Consolidate position and await extraction

**Key Features:**
- Multiple enemy waves with escalating difficulty
- Cooperative wingmate support
- Dynamic enemy spawning
- Time limit and health thresholds

**Rewards:**
- Mission completion unlocks Mission 3
- Bonus for no allied losses
- High score for minimal damage taken

#### Mission 3: Strike
**Difficulty:** Medium-Hard  
**Objective:** Conduct deep strike on enemy airfield

**Primary Objectives:**
1. Navigate to enemy airfield
2. Destroy SAM site (air defense)
3. Attack enemy fighters on ground
4. Destroy command facility
5. Escape to friendly territory

**Key Features:**
- Heavy enemy air defense
- Coordinated attack with wingmates
- Multiple ground and air targets
- Fuel management critical
- High-intensity combat

**Rewards:**
- Campaign completion
- Elite score rankings
- Unlock additional aircraft/weapons

---

## Mission Progression System

### Progression Tracking

**Missions Track:**
- **Completion status** — Not Started / In Progress / Complete
- **Best score** — Highest score achieved
- **Best time** — Fastest completion time
- **Damage taken** — Lowest damage run
- **Kills** — Total enemies defeated

### Unlocking Missions

**Linear Progression:**
1. Complete Mission 1 → Mission 2 unlocked
2. Complete Mission 2 → Mission 3 unlocked
3. Complete Mission 3 → Campaign complete

**Free Mission Mode:**
- Once campaign complete, can replay any mission
- Unlock at higher difficulties
- Attempt elite challenge scores

---

## Mission Objectives

### Objective Types

#### Navigation Objective
- **Task:** Fly to waypoint or location
- **Success criteria:** Reach location and maintain altitude for 5 seconds
- **UI:** Waypoint marker and distance indicator
- **Typical use:** Getting to engagement area

#### Enemy Elimination Objective
- **Task:** Destroy specified enemy aircraft or ground targets
- **Success criteria:** Target destroyed
- **UI:** Target highlighted; kill confirmation audio/visual
- **Typical use:** Dogfight or air-to-ground combat

#### Protect Objective
- **Task:** Prevent enemy from destroying ally
- **Success criteria:** Protected target survives for duration
- **UI:** Allied position marked; threat indicator
- **Typical use:** Convoy protection, base defense

#### Collect Intelligence Objective
- **Task:** Photograph or identify target location
- **Success criteria:** Target scanned/photographed; intel collected
- **UI:** Collection point marked; scanning progress
- **Typical use:** Reconnaissance missions

#### Survive Objective
- **Task:** Survive for specified duration
- **Success criteria:** Time expires; player still alive
- **UI:** Timer on HUD
- **Typical use:** Extended air battles

#### Escort Objective
- **Task:** Accompany and protect ally
- **Success criteria:** Ally reaches destination alive
- **UI:** Formation indication; waypoint marker
- **Typical use:** Bomber escort or VIP protection

### Objective Display

On HUD during mission:
- **Primary objective:** Main text at top of screen
- **Waypoint marker:** Indicates objective location
- **Distance:** Kilometers to objective
- **Status:** Progress indicators (e.g., "2/3 targets destroyed")
- **Timer:** Time remaining (if time-limited)

### Objective Completion

When objective completes:
1. **Audio cue** — Success tone or failure message
2. **HUD update** — Next objective appears
3. **Visual feedback** — Waypoint updates
4. **Score update** — Points awarded for completion

---

## Mission Mechanics

### Mission Start

**Pre-Mission Screen:**
1. **Select aircraft** — Choose from available inventory
2. **Select loadout** — Choose weapons/fuel configuration
3. **Select difficulty** — Normal/Advanced/Ace
4. **Review briefing** — Read mission objectives
5. **Start mission** — Launch into level

### Spawn Process

1. **Mission intro** — Briefing video or radio callout
2. **Player spawn** — Aircraft appears in-game (usually airborne)
3. **Radio callout** — Mission controller provides initial instructions
4. **Objectives active** — Navigation/objective markers appear
5. **Ready to engage** — Player takes control

### During Mission

- **Objectives track** on HUD throughout flight
- **Radio callouts** — Mission controller provides updates
- **Wingmates support** — AI pilots assist as assigned
- **Enemy presence** — Fighters and ground targets engage
- **Environmental effects** — Weather, time of day effects

### Mission End

**Success:**
1. **Final objective complete** — Last objective accomplished
2. **Mission complete message** — Success audio/visual
3. **Extract waypoint** — Return to base marked
4. **Results screen** — Score, statistics, rewards displayed

**Failure:**
1. **Failure condition met** — Player eliminated, objective failed, timeout
2. **Mission failed message** — Failure audio/visual
3. **Retry option** — Restart mission or return to menu

---

## Mission Difficulty

### Difficulty Scaling

| Aspect | Normal | Advanced | Ace |
|--------|--------|----------|-----|
| **Enemy AI** | Normal | Advanced | Ace |
| **Enemy numbers** | Standard | 150% | 200% |
| **Friendly AI help** | Enhanced | Standard | Minimal |
| **Objective timers** | Generous | Standard | Strict |
| **Fuel availability** | Abundant | Standard | Limited |
| **Air defense** | Moderate | Heavy | Overwhelming |
| **Margin of error** | Large | Medium | None |

### Dynamic Difficulty

Some missions adjust difficulty:
- **If player struggling** — Enemy reinforcements delayed, more fuel available
- **If player dominating** — Enemy reinforcements arrive sooner, harder AI
- **Per-objective basis** — Individual objectives can have adjustable difficulty

---

## Mission Rewards & Scoring

### Scoring System

Points awarded for:
- **Mission completion** — Base points (varies by difficulty)
- **Enemy elimination** — Points per kill
- **Objective bonuses** — Bonus for time/efficiency
- **No damage bonus** — Bonus for completing without damage
- **High score bonus** — Bonus for beating previous best

### Scoring Formula
```
Base Score (difficulty multiplier)
+ (Kills × 100)
+ Time Bonus (faster = more points)
+ No Damage Bonus (500 points if no damage)
+ Efficiency Bonus (fuel saved bonus)
= Final Score
```

### Difficulty Multipliers
- Normal: 1.0×
- Advanced: 1.5×
- Ace: 2.0×

### Leaderboards

**Per-Mission Leaderboards:**
- Global top 100 scores
- Regional rankings
- Difficulty-specific rankings
- Time-based rankings (speedrun)

**Campaign Leaderboards:**
- Total campaign score
- Campaign completion time
- No-death runs

### Rewards

**For Completion:**
- Achievement/trophy unlock
- Currency for cosmetics
- XP for progression
- New aircraft/weapon unlock (first time)

**For High Scores:**
- Cosmetic rewards
- Bragging rights
- Leaderboard ranking

---

## Radio & Narrative

### Mission Briefing

**Pre-mission:**
- **Radio operator** provides mission objectives
- **Tactical situation** — Enemy positions and composition
- **Friendly support** — Wingmate assignments and support
- **Time constraints** — Mission duration and deadlines
- **Special notes** — Unique hazards or opportunities

### In-Mission Radio Callouts

**Common callouts:**
- **"Bandits in the area"** — Enemy fighters detected
- **"Target eliminated"** — Objective completed
- **"Objective failed"** — Objective can't be completed
- **"Fuel status"** — Low fuel warning
- **"Wingmate down"** — Ally eliminated
- **"Target marked"** — Waypoint identified

### Radio Discipline

Radio communications simulate realistic military protocol:
- **Callsigns** — Player has assigned callsign (e.g., "Viper 1")
- **Communication brevity** — Realistic military radio traffic
- **Frequency management** — May switch frequencies for different zones
- **Radio etiquette** — Player radio discipline affects immersion

---

## Wingmate System in Missions

### Wingmate Assignment

**Standard assignment:**
- **Mission 1:** 0-1 wingmate (learning mission)
- **Mission 2:** 1-2 wingmates (support against multiple enemies)
- **Mission 3:** 2 wingmates (deep strike support)

### Wingmate Orders

**Player can command wingmates:**
- **"Follow me"** — Maintain formation
- **"Break and engage"** — Attack nearby targets
- **"Rejoin"** — Return to formation
- **"Watch my six"** — Focus on rear defense

### Wingmate Behavior

- **Defend player** — Intercept threats to player
- **Attack targets** — Engage enemy fighters
- **Maintain formation** — Fly in tactical formation
- **Radio callouts** — Provide tactical updates
- **Coordinate attacks** — Focus fire on single targets

---

## Extended Missions & Campaigns

### Custom Missions

Developers can create custom missions:
1. Create level with spawn points
2. Configure objective sequence
3. Set enemy encounters and scripting
4. Define reward thresholds
5. Test and publish

### Mission Customization

- **Objectives** — Define primary, secondary, hidden objectives
- **Time limits** — Optional mission timer
- **Waves/encounters** — Scripted or random enemy spawning
- **Waypoints** — Navigation markers for player
- **Audio** — Mission briefing and in-mission callouts
- **Rewards** — Points, unlocks, progression

---

## Mission Tips & Strategies

### Pre-Mission Planning

1. **Read briefing** — Understand objectives
2. **Choose aircraft** — Pick for mission type (balanced/specialized)
3. **Select loadout** — Rockets for ground, missiles for air
4. **Check difficulty** — Start lower if learning mission
5. **Plan route** — How to reach objectives efficiently

### During Mission

1. **Follow objectives** — Complete in order marked
2. **Manage fuel** — Plan landing/refuel points
3. **Watch six** — Keep checking for threats
4. **Coordinate with wingmates** — Use them effectively
5. **Adapt on the fly** — Adjust strategy if circumstances change

### Mission Completion

1. **Extract safely** — Complete mission return waypoint
2. **Assess damage** — Minimize damage for bonus points
3. **Compare score** — Can you beat previous best?
4. **Unlock next** — Progression to next mission/difficulty

---

## Troubleshooting Missions

### Mission Won't Start
**Cause:** Previous mission not complete; technical issue
**Solution:**
1. Verify previous mission is marked complete
2. Restart mission selection
3. Restart application if problem persists

### Objective Won't Complete
**Cause:** Success conditions not met; bug
**Solution:**
1. Verify objective completion criteria (distance, time, etc.)
2. Return to objective area
3. Try alternative approach
4. Restart mission if stuck

### Wingmates Not Helping
**Cause:** Wingmates performing poorly; out of position
**Solution:**
1. Issue "Rejoin" command to regroup
2. Position yourself for support
3. Manually assist by focusing on objectives
4. Reduce difficulty if wingmates ineffective

### Mission Too Difficult
**Cause:** Difficulty setting too high; enemy overwhelming
**Solution:**
1. Restart at lower difficulty
2. Practice flight and combat in training
3. Improve dogfighting skills before retry
4. Use wingmates more effectively

---

## Next Steps

- **Master flight:** [Flight & Cameras](FLIGHT_AND_CAMERAS.md)
- **Learn combat:** [Weapons & Targeting](WEAPONS_AND_TARGETING.md)
- **Challenge AI:** [AI System](AI_SYSTEM.md)
- **Setup multiplayer:** [Multiplayer](MULTIPLAYER.md)

---

**Accept the mission. Achieve the objectives. Complete the campaign.**
