# AI System Guide

## AI Fighter Overview

Aerial Thunder features intelligent AI opponents with adaptive difficulty, tactical decision-making, and realistic dogfighting behavior. The AI system is modular and extensible, allowing developers to create custom AI behaviors.

---

## Difficulty Levels

### Normal Difficulty
**Designed for:** Learning players, casual gameplay

#### Characteristics
- **Accuracy:** 40-50% gun accuracy
- **Missiles:** Fires 1-2 missiles per engagement
- **Tactics:** Basic pursuit, occasional evasion
- **Reaction time:** ~1-2 seconds
- **Energy management:** Poor; often stalls or overspeeds
- **Teamwork:** Minimal coordination with other AI

#### AI Behavior
- **Predictable:** Follows relatively consistent patterns
- **Slow to adapt:** Takes time to adjust to player tactics
- **Forgiving:** Makes mistakes that experienced players can exploit
- **Learning curve:** Good for understanding AI behavior

### Advanced Difficulty
**Designed for:** Experienced players, competitive gameplay

#### Characteristics
- **Accuracy:** 60-70% gun accuracy
- **Missiles:** Fires multiple missiles; uses saturation tactics
- **Tactics:** Advanced maneuvers, energy management, positioning
- **Reaction time:** ~0.5-1 second
- **Energy management:** Good; maintains altitude/energy advantage
- **Teamwork:** Coordinates with other AI wingmates

#### AI Behavior
- **Challenging:** Consistently outmaneuvers rookie tactics
- **Adaptive:** Recognizes player strategy and counters
- **Skilled:** Executes complex maneuvers with precision
- **Demanding:** Requires advanced flight skills to defeat

### Ace Difficulty
**Designed for:** Expert players, maximum challenge

#### Characteristics
- **Accuracy:** 80%+ gun accuracy
- **Missiles:** Continuous missile employment; expert tactics
- **Tactics:** Master-level dogfighting, ambush tactics, energy traps
- **Reaction time:** Instant to 0.5 seconds
- **Energy management:** Expert; never wastes energy
- **Teamwork:** Flawless coordination; superior tactics

#### AI Behavior
- **Brutal:** Nearly unbeatable for average players
- **Exploitative:** Punishes poor decisions instantly
- **Merciless:** No hesitation; no mercy
- **Expert pilot:** Behaves like fighter pilot with decades of experience

---

## AI Tactical Behaviors

### Pursuit Phase
AI closes distance to target:
1. **Target acquisition** — Identifies and locks on
2. **Range closure** — Accelerates toward target
3. **Energy management** — Maintains altitude advantage
4. **Positioning** — Jockeys for superior position
5. **Attack initiation** — Begins gun or missile employment

### Attack Phase
AI executes weapons employment:
1. **Gun attack** — Closes to optimal range for gun fire
2. **Missile employment** — Launches guided missiles
3. **Multi-pass** — If first pass unsuccessful, repositions for second pass
4. **Damage assessment** — Evaluates hit/miss results

### Evasion Phase
AI responds to incoming threats:
1. **Lock detection** — AI detects enemy lock tone
2. **Threat assessment** — Evaluates missile threat level
3. **Flare deployment** — Dispenses countermeasures
4. **Hard maneuver** — Executes evasive maneuver
5. **Disengagement** — May climb or turn away from threat

### Defensive Phase
AI focuses on survival:
1. **Defensive posture** — Wings level, predictable flight
2. **Evasion turn** — Tight turn to break pursuit
3. **Altitude** — Climbs or descends to optimal defensive altitude
4. **Fuel check** — May disengage to preserve fuel
5. **Regrouping** — Rejoins with friendly AI or retreats to base

---

## AI Decision-Making

### Threat Assessment
AI evaluates multiple factors:
- **Distance to enemy** — Closer = more urgent threat
- **Enemy heading** — Pointing at AI = higher threat
- **AI fuel status** — Low fuel = deprioritize combat
- **AI damage status** — Heavy damage = avoid engagement
- **Ally support available** — Odds of winning engagement
- **Mission priority** — Primary objective vs. combat engagement

### Tactical Decision Tree
```
AI Encounters Player
  ├─ Assess threat level
  │  ├─ High threat → Evade or disengage
  │  ├─ Medium threat → Prepare defensive stance
  │  └─ Low threat → Pursue aggressively
  ├─ Evaluate engagement odds
  │  ├─ Favorable → Attack
  │  ├─ Balanced → Cautious approach
  │  └─ Unfavorable → Disengage
  └─ Execute chosen tactic
     ├─ Missile employment
     ├─ Gun attack
     ├─ Evasion maneuver
     └─ Disengagement
```

### Learning Algorithm (Advanced/Ace Only)
AI remembers player tactics and adapts:
- **Learns preferred maneuvers** — Recognizes scissors, immelman, split-S, etc.
- **Counters tactics** — Adjusts flight path to counter learned maneuvers
- **Predicts movements** — Anticipates where player will move next
- **Exploits weaknesses** — Targets identified weak areas of player performance

---

## AI Combat Tactics

### Scissors Maneuver
AI initiates mutual turn:
1. **Both aircraft turn toward each other**
2. **AI attempts to out-turn player**
3. **If successful, gains six o'clock position**
4. **If unsuccessful, reverses and tries opposite direction**

### Energy Trap
AI uses altitude and speed advantage:
1. **AI climbs above player**
2. **AI dives down with speed advantage**
3. **AI attempts gun pass from above**
4. **AI pulls back up to regain altitude before player can counterattack**

### Vertical Loop
AI uses vertical maneuver for advantageous re-engagement:
1. **AI climbs vertically (if energy permits)**
2. **Completes loop at top of arc**
3. **Re-engages from fresh direction**
4. **Maintains energy throughout**

### Ambush Tactic
AI (especially Ace difficulty) coordinates attacks:
1. **First AI attracts player attention**
2. **Second AI attacks from unexpected direction**
3. **Player caught between two attackers**
4. **Difficult to escape; requires quick thinking**

### Missile Saturation
AI fires multiple missiles in sequence:
1. **First missile fired**
2. **AI immediately locks second target**
3. **Second missile fired**
4. **Player forced to deploy flares and maneuver**
5. **Multiple missiles increase hit probability**

---

## AI Difficulty Scaling

### What Changes with Difficulty

| Aspect | Normal | Advanced | Ace |
|--------|--------|----------|-----|
| **Reaction Time** | 1-2 sec | 0.5-1 sec | Instant |
| **Accuracy** | 40-50% | 60-70% | 80%+ |
| **Missiles/Pass** | 1-2 | 2-3 | 3-4 |
| **Flare Usage** | Reactive | Proactive | Optimal |
| **Energy Mgmt** | Poor | Good | Expert |
| **Prediction** | None | Basic | Expert |
| **Coordination** | Solo | Some | Perfect |

### Dynamic Difficulty Adjustment
During missions, AI difficulty can scale:
- **If player is dominating** — AI gradually becomes more skilled
- **If player is struggling** — AI may reduce difficulty
- **Per-mission setting** — Can be locked at difficulty level
- **Per-AI setting** — Individual AI units can have different difficulties

---

## AI Wingmate System

### Wingmate Assignment
In missions and multiplayer:
- **Player spawns as lead** — Player commands wingmates
- **Wingmates follow** — Usually 1-2 AI pilots assigned to player
- **Radio callouts** — Wingmates provide tactical callouts

### Wingmate Communications

#### Wingmate Callouts
- **"Bandits at twelve o'clock"** — Enemies spotted ahead
- **"Missile in the air"** — Incoming missile detected
- **"Break right / left"** — Evasive maneuver recommendation
- **"Enemy six"** — Attacker behind player
- **"I've got a target"** — Wingmate engaging enemy

#### Player Commands
- **VoIP or key bindings** — Issue orders to wingmates
- **"Follow me"** — Wingmates maintain formation
- **"Break and engage"** — Wingmates attack nearby targets
- **"Rejoin"** — Wingmates return to formation

### Wingmate Tactics
- **Mutual support** — If wingmate is attacked, others provide cover
- **Coordinated attacks** — Multiple wingmates attack single target
- **Formation flying** — Maintain tactical formation for mutual defense
- **Fuel monitoring** — Wingmates track fuel and suggest landing

---

## AI Configuration

### Per-Mission AI Settings

In mission setup or editor:
- **AI Count** — Number of enemy AI fighters
- **AI Difficulty** — Normal/Advanced/Ace
- **AI Loadouts** — Varied or standardized
- **AI Behavior** — Aggressive/Defensive/Balanced
- **Wingmate Assignment** — How many wingmates assigned to player

### Per-Aircraft AI Customization

Developers can modify AI behavior via:
- **C++ classes** — Custom AI behavior trees
- **Blueprints** — Visual AI logic graphs
- **Configuration files** — Parameter tuning

---

## AI Challenges & Scenarios

### Training Scenarios

#### Dogfight Arena
- **Setup:** 1v1 engagement
- **Difficulty:** Selectable
- **Objective:** Defeat single opponent
- **Best for:** Learning dogfighting basics

#### Two vs. Two
- **Setup:** 2 players vs. 2 AI
- **Difficulty:** Selectable
- **Objective:** Coordinate with teammate
- **Best for:** Teamwork and communication

#### Survival Challenge
- **Setup:** 1 player vs. multiple AI
- **Difficulty:** Escalates as player gains kills
- **Objective:** Survive as long as possible
- **Best for:** Advanced combat skills

### Mission-Based AI Challenges

#### Formation Defense
- **Scenario:** Protect friendly formation from attackers
- **AI behavior:** Coordinated attack on formation
- **Difficulty:** Variable by mission difficulty

#### Overland CAP (Combat Air Patrol)
- **Scenario:** Defend assigned area from multiple AI fighters
- **AI behavior:** Intrusion attempts and aggressive engagement
- **Difficulty:** More intrusions at higher difficulty

---

## AI Limitations & Workarounds

### AI Doesn't Exploit Physics
- **Limitation:** AI doesn't abuse network lag or exploits
- **Design:** Fair and balanced gameplay
- **Impact:** AI plays by same rules as players

### AI Respects Flight Envelope
- **Limitation:** AI can't violate aircraft flight limits
- **Design:** Realistic physics for both AI and player
- **Impact:** No superhuman maneuvers

### AI Can Be Baited
- **Limitation:** Aggressive AI can be lured into terrain or disadvantage
- **Tactic:** Experienced players can bait AI into poor positioning
- **Counterplay:** Higher AI difficulty learns these tactics

---

## Beating Different AI Difficulties

### Beating Normal AI

1. **Turn fight advantage** — Scissors maneuver to gain position
2. **Gun accuracy** — Normal AI has poor accuracy; close for easy kills
3. **Missile defense** — Single missile easily evaded with flares
4. **Predictability** — Anticipate moves; execute counters
5. **Energy advantage** — Out-turn AI; maintain altitude

### Beating Advanced AI

1. **Energy management** — Match AI's altitude/speed management
2. **Multi-pass tactics** — Don't expect one-pass kills; plan multiple passes
3. **Missile saturation** — Prepare for 2-3 missile passes; have flares ready
4. **Coordination** — Use wingmates effectively
5. **Positioning** — Gain and maintain six o'clock position

### Beating Ace AI

1. **Perfection required** — One mistake can be fatal
2. **Flare usage** — Deploy flares proactively; don't wait for missiles
3. **Ambush tactics** — Use terrain and surprise
4. **Teamwork essential** — Coordinate with wingmates for mutual support
5. **Energy discipline** — Never allow AI to gain altitude advantage
6. **Vertical escape** — If losing, climb vertically to gain separation

---

## AI Troubleshooting

### AI Seems Too Easy
**Solution:**
1. Increase difficulty in mission settings
2. Increase number of enemy AI
3. Try Ace difficulty
4. Fight against multiple AI simultaneously

### AI Seems Impossible
**Solution:**
1. Reduce difficulty to Normal
2. Use Advanced Flight mode instead of Arcade (more control)
3. Practice in training scenarios first
4. Ask wingmates for help by coordinating attacks
5. Review dogfighting tactics in guides

### AI Behavior Seems Broken
**Cause:** AI is behaving unexpectedly or irrationally
**Solution:**
1. Verify mission settings are correct
2. Check if AI is in spawning state (may appear to freeze)
3. Restart mission
4. If persistent, report via troubleshooting channels

---

## Tips for AI Combat

1. **Learn one difficulty at a time** — Don't jump to Ace immediately
2. **Study AI patterns** — Watch AI behavior before engaging
3. **Use superior tactics** — Scissors, energy traps, vertical maneuvers
4. **Protect your six** — AI loves attacking from behind
5. **Fuel matters** — If AI fuel runs low, it will disengage
6. **Flares are free** — Use them liberally; they're cheap insurance
7. **Teamwork wins** — Coordinating with wingmates dramatically improves odds
8. **Respect the AI** — Ace AI is truly dangerous; treat with caution
9. **Practice regularly** — Dogfighting skills improve with repetition
10. **Learn from losses** — Each defeat teaches something new

---

## Next Steps

- **Master flight:** [Flight & Cameras](FLIGHT_AND_CAMERAS.md)
- **Learn weapons:** [Weapons & Targeting](WEAPONS_AND_TARGETING.md)
- **Read radar:** [HUD & Radar](HUD_AND_RADAR.md)
- **Complete missions:** [Mission System](MISSION_SYSTEM.md)

---

**Face the AI. Learn from defeat. Become the ace.**
