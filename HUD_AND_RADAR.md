# HUD and Radar Guide

## Overview

The sample jet includes a working cockpit HUD, a tactical radar display, automatic targeting UI, and a manual Tactical Air Display. These systems are configurable and designed to support single-player targets, AI aircraft, and multiplayer jets.

This is a gameplay radar and targeting implementation. It does not simulate pulse, pulse-Doppler, track-while-scan, radar cross-section, or electronic warfare modes.

## Cockpit HUD

The HUD presents the flight and combat information configured by the supplied jet Blueprint and HUD widget. The exact layout can be redesigned without changing movement or weapon authority.

Depending on the configured widget, the HUD can present:

- flight references,
- targeting information,
- weapon and ammo state,
- waypoint and objective information,
- warning feedback,
- tactical radar contacts.

Do not rely on generated documentation for a fixed list of gauges. Inspect the supplied HUD widget and the jet's bound values before replacing its layout.

## Tactical Radar

`UJetTacticalRadarComponent` gathers nearby configured contacts and sends them to the radar widget.

### Supported Contact Sources

- ground target actors,
- air target actors,
- player-controlled jets,
- AI-controlled jets,
- additional configured actor classes.

### Team Colors

Radar colors are team-aware:

- friendly contacts use the configured friendly color,
- enemy contacts use the configured enemy color,
- neutral contacts are optional and use the configured neutral color.

The radar can resolve multiplayer jet teams from pawn state. AI pilot jets can be treated as enemies. Ground and air targets retain their configured team behavior on both host and client.

### Radar Configuration

The component exposes:

- enable/disable,
- owner team ID,
- automatic owner-team resolution,
- radar range,
- update rate,
- maximum contacts,
- friendly/enemy/neutral visibility,
- automatic jet-pawn inclusion,
- AI-as-enemy handling,
- heading-up behavior,
- target actor classes,
- contact colors,
- debug output.

### Radar Visibility by Camera

The radar widget can be configured independently for:

- cockpit view,
- shoulder view,
- chase view.

The sample defaults favor cockpit and shoulder visibility. Change these options in the radar component rather than duplicating widgets per camera.

## Automatic Targeting UI

Automatic targeting uses the standard forward lock presentation.

It can show:

- the current target,
- a target lock box,
- acquisition and lock state,
- lock confirmation feedback.

The target lock box's designer size remains visible in the Widget Blueprint editor, while its runtime visibility is controlled by the targeting code. Do not solve runtime visibility by permanently hiding the widget in the designer.

## Manual Tactical Air Display

Manual targeting is a separate cockpit workflow driven by `UJetManualTargetingComponent`.

It uses a scene capture and TAD display for:

- finding a target through the cockpit display,
- manual focus selection,
- manual lock on/off,
- guided missile employment from a manual lock.

The manual system exposes capture resolution/performance controls, camera FOV, target filtering, focus behavior, aim behavior, and lock settings.

When manual targeting is active:

- the automatic targeting widget is hidden,
- automatic lock audio is suppressed,
- the player uses the TAD workflow instead.

## Warning System

The jet warning system includes ground-proximity and combat feedback. Warning playback uses state checks and cooldowns to prevent repeated fragments such as overlapping altitude or pull-up calls.

Warning behavior is designed for fast aircraft and can be tuned for:

- detection distance,
- warning thresholds,
- repeat cooldowns,
- audio assignment,
- debug output.

Keep warning audio local to the affected pilot unless a specific exterior sound is intended for nearby players.

## Waypoints and Mission Feedback

Mission waypoints and status text are owned by the mission framework rather than the tactical radar component.

The mission system supports:

- ordered waypoints,
- pass radius,
- objective text,
- visual state changes,
- hiding or destroying a passed waypoint,
- mission state and target-count updates.

See [MISSION_SYSTEM.md](MISSION_SYSTEM.md) for setup.

## Multiplayer Behavior

Radar and targeting state must agree with replicated team and pawn information.

Expected behavior:

- each player sees friendly and enemy multiplayer jets using the correct colors,
- AI jets appear as enemies when configured,
- ground and air target colors remain consistent between host and client,
- automatic lock UI and audio are local to the controlling player,
- manual TAD capture runs only where needed.

The tactical radar is primarily a local presentation system. Do not replicate the entire radar widget or every UI update.

## Blueprint Integration

For a derived jet Blueprint:

1. Keep the tactical radar component attached to the jet.
2. Assign the intended radar widget name.
3. Configure target classes and team behavior.
4. Set the desired camera visibility options.
5. Confirm the HUD contains the expected radar widget.
6. Configure automatic targeting widgets and sounds.
7. Configure the manual TAD capture and display.

## Troubleshooting

### AI appears friendly

- Enable AI pilot jets as enemy contacts.
- Verify the AI radar signature team override.
- Check the AI team ID and the local player's team ID.
- Confirm the project includes the current AI radar correction.

### Host and client see different target colors

- Verify team state replicates before radar refresh.
- Enable automatic team resolution from pawn state.
- Check target Blueprint team IDs.
- Force a radar refresh after team assignment when testing custom spawn flows.

### The lock box is always visible

- Keep the designer widget visible so its size can be edited.
- Let the targeting component control runtime visibility.
- Remove duplicate Blueprint visibility bindings.

### Manual mode hides the UI but lock audio continues

- Enable targeting-audio suppression for manual lock.
- Confirm the mode switch deactivates automatic targeting cleanly.
- Check for audio started independently in the Widget Blueprint.

### Radar is empty

- Enable the tactical radar component.
- Increase the configured range for testing.
- Verify contact classes and tags.
- Check friendly/enemy/neutral visibility filters.
- Confirm the radar widget name matches the HUD widget.

### TAD capture is expensive

- Lower its configured capture resolution or update frequency.
- Activate it only during manual targeting.
- Avoid running manual capture on remote or AI jets that do not need it.

## Related Guides

- [WEAPONS_AND_TARGETING.md](WEAPONS_AND_TARGETING.md)
- [FLIGHT_AND_CAMERAS.md](FLIGHT_AND_CAMERAS.md)
- [MISSION_SYSTEM.md](MISSION_SYSTEM.md)
- [UI_AND_SETTINGS.md](UI_AND_SETTINGS.md)
- [MULTIPLAYER.md](MULTIPLAYER.md)
