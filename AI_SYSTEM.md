# AI System

This guide covers the included fighter AI, activation modes, difficulty presets, attack behavior, weapons, defenses, avoidance, and mission integration.

## Core Component

`UJetAIPilotComponent` is a server-authoritative AI pilot input generator for `AJetPawn`.

The AI does not use a separate simplified aircraft actor. It drives the same jet movement and weapon systems used by a player aircraft. `ApplyAIFlightInput` feeds pitch, roll, yaw, throttle, air brake, and related control into the normal simulation/replication path.

Add `UJetAIPilotComponent` to an AI jet Blueprint and configure it in the `Jet|AI Pilot` categories.

## Authority

- The AI brain runs on the server.
- Target selection and weapon decisions are authoritative.
- The AI jet replicates through the same movement presentation used by other jets.
- Clients receive the result; they do not run competing AI decisions.

## Pilot Modes

`EJetAIPilotMode` includes:

| Mode | Behavior |
|---|---|
| Disabled | AI input generation is off. |
| Orbit Around Spawn | Patrol/orbit near the initial area. |
| Chase Nearest Jet | Search for and pursue a valid jet target. |
| Orbit + Chase Nearest Jet | Patrol until a target is available, then pursue it. |

The component exposes activation and target assignment functions for Blueprint/C++ integration, including explicit target control and automatic nearest-target behavior.

## Difficulty Presets

`EJetAIDifficultyPreset` includes:

- Custom
- Easy
- Normal
- Hard
- Ace

Use `SetDifficultyPreset`, `SetDifficultyPresetByName`, or `ApplyDifficultyPreset` to apply a preset at runtime. `bApplyDifficultyPresetOnBeginPlay` controls whether the component applies its selected preset during startup.

The shipped root menu presents a simpler player-facing choice (Normal or Advanced). That menu selection is translated into the configured runtime AI setup; the full component still supports the detailed preset enum above.

### Custom Difficulty

Choose `Custom` when you want all AI values to remain under direct Blueprint control. This is useful for mission-specific enemies, bosses, training aircraft, or non-combat patrols.

## Detection and Chase

Targeting/chase settings include:

- search/update timing
- scan and chase range
- target filtering
- lead time
- direction smoothing
- preferred spacing
- throttle and desired speed
- radar signature team override

Advanced/Ace tuning can maintain pressure on a fast player by increasing chase distance, desired speed, six-pressure behavior, and weapon-pass opportunities.

## Attack Behavior

The component supports gun attacks, missile attacks, attack cycles, and staged attack passes.

`EJetAIAttackPassState` includes:

1. Reposition
2. Approach High
3. Attack Dive
4. Weapon Pass
5. Extend Away
6. Climb Out

Attack-pass settings control distances, altitude, duration, aim height, throttle, speed, extension, and climb-out behavior.

### Gun Attacks

Gun settings include:

- enable/disable attack
- minimum/maximum range
- aim cone and lead time
- line-of-sight requirement
- burst timing and cooldown
- weapon-pass firing behavior

Gun damage can be tuned per difficulty. Keep the server weapon component authoritative; the AI component decides when to fire.

### Missile Attacks

Missile settings include:

- lock and fire range
- lock cone and lead time
- required lock time
- attack cooldown
- line-of-sight requirement
- lock reset rules
- target warning timing

The AI uses the same missile and flare gameplay systems as the player jet.

## Sky Dogfight and Six Pressure

Sky-dogfight settings extend the standard attack pass for sustained air combat. Six-pressure behavior helps the AI stay dangerous when it is behind the player.

Tune these settings together:

- weapon-pass duration and gun range
- too-close breakaway distance
- attack and extension speed
- rear-cone/forward-cone thresholds
- six-pressure maximum distance
- chase smoothing

Very high speed without adequate turn/avoidance distance can increase terrain risk. Test these values in the most complex level, not only over open water.

## Defensive Behavior

The AI can react to:

- incoming missiles with flares
- damage/taking fire
- threats in its rear cone
- unsafe target spacing
- terrain and obstacle probes

Defense settings include reaction delays, cooldowns, evade behavior, flare timing, and counter-chase choices.

## Terrain and Obstacle Avoidance

Avoidance uses forward and directional sensor probes. The system is designed to interrupt free dogfight movement only when a collision threat is detected.

When a threat is detected, the AI can:

- bias steering toward a safe direction
- level/recover from an unsafe inverted attitude
- climb or break away
- maintain clearance long enough to escape
- rejoin the chase after the danger clears

The Details panel exposes avoidance distance, probe shape/spread, predictive look-ahead, clearance, recovery, and steering/throttle behavior.

### Preventing Terrain Crashes

If the AI crashes while following a player through terrain:

1. Increase predictive/forward probe distance for the AI's actual top speed.
2. Increase minimum clearance and recovery hold time.
3. Verify the configured trace channel blocks terrain and buildings.
4. Test inverted, high-pitch, and high-roll approaches.
5. Reduce turn aggression only if the sensors cannot create enough escape time.

Avoidance must be evaluated in aircraft-local danger directions, not as a world-up-only pull-up rule.

## Grounded Targets

The component includes grounded-target policy settings. The polished default project suppresses unsafe close attack behavior against grounded jets to avoid repeated low-altitude circles and crashes. For custom strafing missions, use a designed long-range attack-pass setup with sufficient approach, weapon, extension, and climb-out distance.

## Victory Showcase

After eliminating its target, the AI can perform a controlled victory pass instead of immediately returning to unstable close circling.

`Victory Showcase` settings include:

- enable/disable
- total duration
- initial straight extension
- bank duration and turn amount
- altitude gain
- throttle and desired speed
- randomized bank side

This presentation is also visible during the killed-in-action spectator sequence.

## AI Audio

AI gun, missile, and flare sounds use exterior/remote audio. Assign spatial Sound Attenuation assets and keep remote audible distances appropriate for the effect.

If an AI flare or gun sounds close from a long distance, inspect the AI jet's `JetAudioComponent` assignments and attenuation override before changing combat logic.

## Mission Integration

For a mission:

1. Place an AI jet or configure the Mission/GameMode AI spawner.
2. Assign the AI jet class and a valid `PlayerStart`/spawn tag.
3. Select pilot mode and difficulty.
4. Assign team/radar signature settings.
5. Keep the AI inactive or targets hidden until the mission phase requires combat.
6. Count AI destruction through the mission's configured required targets/objectives.

Mission 03 demonstrates radio, waypoint activation, target reveal, AI combat, action music, objective tracking, and mission results without requiring level-graph wiring.

## Recommended Test Matrix

1. Easy/Normal pursuit and escape opportunity.
2. Advanced/Ace sustained chase at full player speed.
3. Gun aim and burst behavior.
4. Missile lock, warning, fire, and flare defense.
5. Damage reaction and rear-cone defense.
6. Low terrain, buildings, islands, and inverted approaches.
7. Target destroyed, victory showcase, spectating, and respawn.
8. Standalone and listen-server/client replication.

## Screenshot Placeholders

- AI pilot component overview
- Difficulty preset and weapon damage
- Gun and missile attack settings
- Attack pass / sky dogfight / six pressure
- Predictive avoidance sensors
- Victory showcase settings

See also: [Weapons and Targeting](WEAPONS_AND_TARGETING.md), [HUD and Radar](HUD_AND_RADAR.md), and [Architecture](ARCHITECTURE.md).
