# AI System Guide

## Overview

Aerial Thunder includes an authority-run fighter AI implemented by `UJetAIPilotComponent`. The AI uses the same jet, movement, targeting, weapon, audio, health, and radar systems used elsewhere in the project.

The AI is built for combat encounters, Mission 03, and custom extensions. It is highly configurable in Blueprint and does not require an external behavior tree for the supplied workflow.

## Authority and Activation

By default, AI combat logic runs on the server. The resulting aircraft movement, weapons, damage, FX, and audio are then replicated or presented to clients through their owning systems.

Important activation options include:

- AI enabled state,
- pilot mode,
- authority-only execution,
- disabling uncontrolled player flight on the owner,
- disabling AI when the pawn is possessed,
- automatic activation,
- radar signature team override.

## Pilot Modes

The AI supports configurable operating modes, including orbit and chase behavior. It can begin in a patrol/orbit state, detect a valid target, pursue it, attack, break away, and reacquire.

The target can also be cleared or assigned through the exposed Blueprint API.

## Difficulty Presets

The component contains these internal presets:

- Custom,
- Easy,
- Normal,
- Hard,
- Ace.

The sample main menu intentionally exposes a simpler player-facing choice:

| Menu option | Intended AI experience |
|---|---|
| Normal | More forgiving combat |
| Advanced | Stronger chase and attack behavior |

The game mode applies the selected menu difficulty when spawning AI. Developers can expose all internal presets if desired.

### Difficulty Damage

Gun and missile damage can be overridden by difficulty. The values are Blueprint-editable. The supplied Ace configuration is intentionally lethal, including a missile value suitable for a one-hit kill against the sample player health setup.

Do not assume these values suit every derived aircraft. Rebalance them with the target health component.

## Target Detection and Pursuit

The AI can scan for nearby valid targets using configurable:

- scan interval,
- scan radius,
- required tags,
- player-controlled-jet filtering,
- crashed-target filtering,
- chase lead time,
- chase smoothing,
- preferred distance,
- altitude offset.

Once a valid target is acquired, the AI can continue pursuit beyond the original patrol region according to its advanced chase configuration.

## Gun Attack

Gun behavior includes:

- enable/disable,
- minimum and maximum range,
- aim cone,
- target lead time,
- optional line-of-sight checks,
- burst duration,
- burst cooldown,
- stopping when the target leaves the cone,
- forced gun behavior during attack passes.

The attack-pass settings allow longer firing opportunities without requiring the AI to point perfectly at the target every frame.

## Missile Attack

Missile behavior includes:

- enable/disable,
- lock range,
- fire range,
- lock cone,
- lead time,
- required lock time,
- attack cooldown,
- optional line-of-sight checks,
- lock reset behavior,
- player warning before launch.

After firing, the AI can break away before rejoining the fight.

## Defensive Behavior

The AI reacts to combat threats through:

- missile detection and flare deployment,
- configurable flare reaction delay,
- damage threat notification,
- take-fire reaction cooldown,
- rear-cone danger reaction,
- counter-chase behavior after evasion.

Remote flare and gun sounds use distance-based exterior audio rules, so the player should not hear a distant AI as if it were nearby.

## Attack Cycles and Dogfight Pressure

The AI can alternate between attack and repositioning states instead of continuously steering directly at the player.

Available tuning covers:

- break-away after missile or gun use,
- break-away duration and direction,
- throttle and desired speed,
- reacquisition delay,
- attack-pass start and close distances,
- weapon-pass duration,
- sky dogfight pressure,
- pressure while positioned on the target's six,
- target spacing avoidance.

Advanced settings can make the AI maintain pressure against a fast escaping player. Use these carefully because aggressive pursuit also increases terrain risk.

## Terrain and Obstacle Avoidance

The AI includes forward and directional avoidance probes. During pursuit, the sensor response can override normal chase steering when terrain or an object becomes dangerous.

The avoidance system is intended to:

- detect danger before impact,
- choose an escape direction based on current aircraft orientation,
- break away from the obstacle,
- stabilize the jet,
- rejoin pursuit after clearance.

This is especially important when the player flies low between terrain or structures.

### Honest Limitation

The AI is not guaranteed to survive every possible terrain trap. Extreme speed, inverted flight, very tight spaces, unusual collision, or aggressive last-second player maneuvers can still produce a crash. Increase probe distances and clearance conservatively, then test against the actual level geometry.

## Grounded Player Targets

The current polished AI is focused primarily on air combat. Aggressive attack behavior against a fully grounded player was tested but is not presented as a finished air-strike system.

For missions requiring attacks on grounded players, build a dedicated long-range attack-pass or waypoint-driven air-strike mode rather than forcing the standard dogfight chase to operate near the ground.

## Victory Showcase

After eliminating its target, the AI can perform a configurable victory pass. Options include:

- showcase duration,
- straight extension time,
- bank duration and turn angle,
- altitude gain,
- throttle and desired speed,
- randomized bank side.

This behavior is useful while the defeated player sees the killer through the spectating camera.

## Mission Integration

Mission 03 demonstrates the combat workflow:

1. The player enters the mission and receives radio instructions.
2. The player reaches the combat waypoint.
3. Targets and combat state activate.
4. AI aircraft engage the player.
5. The mission tracks required targets and the timer.
6. Completion or failure shows the result workflow.

AI spawn class, count, start tag, difficulty, and mission behavior are configured through the game and mission setup. See [MISSION_SYSTEM.md](MISSION_SYSTEM.md).

## Blueprint Configuration Areas

The AI component exposes extensive categories for:

- difficulty and weapon damage,
- orbit and patrol,
- target detection,
- chase,
- gun and missile attack,
- missile warnings,
- attack cycles,
- attack passes,
- sky dogfight and six pressure,
- defense and flares,
- avoidance,
- victory showcase,
- debug output.

Change one behavior group at a time and keep a tested checkpoint before major tuning.

## What the AI Does Not Include

The supplied system does not claim:

- machine learning or adaptive learning,
- dynamic difficulty based on player history,
- wingmate voice-command control,
- formation command menus,
- fuel management,
- guaranteed collision avoidance,
- a finished grounded-player air-strike mode.

These can be added as project-specific extensions.

## Troubleshooting

### AI does not acquire the player

- Enable target detection.
- Check scan radius and scan interval.
- Verify required target tags.
- Confirm the player is not marked crashed or invalid.
- Check authority-only execution in multiplayer.

### AI does not fire

- Enable the desired weapon attack.
- Check range, cone, cooldown, and lock time.
- Confirm the loadout has ammo.
- Check optional line-of-sight traces.
- Verify the target health and team configuration.

### AI crashes while chasing

- Increase forward and directional avoidance distances.
- Increase ground clearance and pull-up lead time.
- Confirm traces use a channel that detects the level geometry.
- Reduce chase speed or pressure in very dense terrain.
- Test inverted and steep-pitch approaches, not only level flight.

### AI flies in small unstable circles

- Review orbit radius, chase preferred distance, target spacing, and direction smoothing.
- Confirm a stale target or defensive state is cleared.
- Avoid combining extreme chase pressure with very small orbit values.

### AI feels too weak or too strong

- Confirm the menu selection reaches the spawned AI.
- Apply the intended internal difficulty preset.
- Tune gun and missile damage with player health.
- Adjust chase speed, attack ranges, burst timing, and missile cooldown.

## Related Guides

- [MISSION_SYSTEM.md](MISSION_SYSTEM.md)
- [WEAPONS_AND_TARGETING.md](WEAPONS_AND_TARGETING.md)
- [FLIGHT_AND_CAMERAS.md](FLIGHT_AND_CAMERAS.md)
- [HUD_AND_RADAR.md](HUD_AND_RADAR.md)
- [MULTIPLAYER.md](MULTIPLAYER.md)
