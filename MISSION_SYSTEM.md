# Mission System

## Overview

Aerial Thunder includes a reusable, Blueprint-configured mission framework in the `AT_GM` plugin. Mission logic is driven by placed director actors, waypoint actors, target references, audio beats, timers, saved progression, and result widgets. A mission designer can build or extend missions without placing custom logic in a Level Blueprint.

The included project contains three playable missions:

| Mission | Purpose | Core flow |
|---|---|---|
| Mission 01 | Flight training | Intro sequence, airborne spawn, training waypoints |
| Mission 02 | Takeoff and landing training | Intro sequence, carrier operations, ordered waypoints |
| Mission 03 | Combat mission | Fade-in start, radio sequence, waypoint-triggered combat, required targets, AI, timer, result |

Mission 01 unlocks Mission 02. Mission 02 unlocks Mission 03. Completion state is stored locally through the mission progress save.

---

## Core Actors

### Mission Director

Place a Blueprint derived from `AAT_GM_MissionDirectorActor` in the mission map. It owns the mission state and can:

- Start, stop, complete, or fail the mission.
- Publish objective, status, and notification text to the mission HUD.
- Track ordered waypoints.
- Track explicitly configured required targets.
- Run a mission timer and optionally fail when it expires.
- Play sequential radio/audio beats.
- Start and stop action music with fade times.
- Activate actors when a waypoint is passed.
- Save mission completion and unlock later mission IDs.
- Open complete or failed result UI.
- Configure the next mission map and loading widget.

The director can auto-start on Begin Play and can be restricted to mission travel using `Only Run for Mission Travel`.

### Mission Intro Director

`AAT_GM_MissionIntroDirector` handles the start presentation and player spawn/possession workflow. It supports:

- An optional Level Sequence.
- A no-sequence fallback.
- Fade from black and possession fades.
- Grounded or airborne spawn points.
- Input lock during the intro.
- Applying the stored control mode to the spawned jet.
- An optional Blueprint-callable intro skip.

A Level Sequence is not required. Mission 03 intentionally uses the fade workflow without a sequence.

### Mission Waypoint

`AAT_GM_MissionWaypointActor` is a reusable ordered waypoint with:

- A designer-defined `Waypoint Id`.
- `Waypoint Order` for sorting.
- A configurable pass radius.
- Objective and passed-notification text.
- Built-in M1/M2 visual states.
- Enable/disable control.

The mission director can receive waypoint actors through a configured array or auto-find them using an actor tag. Waypoint IDs are project-defined names such as `A`; they are not hard-coded mission names.

---

## Waypoint Events

Each `FATGM_MissionWaypointEvent` connects a waypoint ID to mission actions. When that waypoint is passed, the event can:

- Hide or destroy the passed waypoint.
- Push new objective/status/notification text.
- Play or queue a dedicated audio sequence.
- Start mission action music.
- Activate configured actors.
- Change activated actors' hidden, collision, and tick states.
- Start required-target tracking.
- Complete the mission when every required target is destroyed.

This is the recommended way to reveal a combat area after the player reaches a navigation point. Keep the actors placed in the level, configure them as inactive/hidden at mission start, then activate them from the waypoint event.

---

## Audio Beats

Mission radio is configured as an array of `FATGM_MissionAudioBeat` entries. Each beat contains:

- `Beat Id`
- `Sound`
- `Delay Before Seconds`
- `Delay After Seconds`
- Optional mission-state text to push when the beat plays

The director can auto-play its main sequence at mission start. A waypoint event can also own a separate sequence, which is useful for an ATC call followed by a delayed pilot response exactly when combat begins.

Action music is configured separately with volume, fade-in, and fade-out values. The director stops mission audio and music when the mission completes, fails, or is stopped.

---

## Required Targets

Required targets are explicit actor references. They can include the supplied ground targets, air targets, and configured AI actors.

Recommended setup:

1. Place the targets in the level.
2. Add them to `Configured Required Targets` or to a waypoint event's `Required Targets`.
3. Enable required-target tracking at mission start or from a waypoint event.
4. Enable completion when all configured targets are destroyed.
5. Set the objective/status text shown while targets remain.

The director observes target destruction and updates the remaining count. It does not invent or dynamically choose mission targets unless the project adds that behavior.

---

## Mission 03 Example

Mission 03 demonstrates the extensible combat workflow:

1. The mission starts with a Blueprint-editable fade from black.
2. ATC and pilot radio beats play in sequence.
3. Waypoint A guides the player into the patrol zone.
4. Passing Waypoint A hides or destroys the waypoint.
5. The waypoint event reveals and activates the configured combat actors.
6. A second ATC/pilot sequence announces weapons clearance.
7. Action music fades in.
8. Required-target tracking begins.
9. The player destroys the configured ground, air, and AI targets before the timer expires.
10. Completion opens the mission result widget and saves progression.

This same pattern can be duplicated for Mission 04, Mission 05, or later missions. Use new mission IDs, maps, waypoint IDs, target references, audio assets, and menu entries rather than changing plugin code.

---

## Results and Progression

The result workflow supports:

- Separate success and failure text.
- Delayed result display.
- Continue flying, restart, main menu, and optional next-mission actions.
- A loading widget during travel.
- A next mission ID, map name, and travel options.

For a next-mission button to appear, configure the current mission director's next mission fields. Menu unlocking is configured independently through mission IDs and prerequisite IDs in the root menu.

Progression stores completion/unlock state locally. It is not a score, reward, rank, achievement, or online leaderboard system.

---

## Blueprint Extension Points

The director exposes Blueprint events for:

- Mission started
- Waypoint passed
- Mission completed
- Mission failed

Use these events for project-specific presentation that is not covered by the generic properties. Keep reusable mission state in the director and avoid Level Blueprint wiring where possible.

---

## Current Scope

The supplied framework includes navigation, target elimination, timers, radio, music, progression, results, actor activation, and AI combat integration. It does not currently include built-in escort logic, photo reconnaissance, wingmate commands, dynamic difficulty, fuel objectives, campaign rewards, or mission scoring.

See also:

- [AI System](AI_SYSTEM.md)
- [HUD and Radar](HUD_AND_RADAR.md)
- [UI and Settings](UI_AND_SETTINGS.md)
