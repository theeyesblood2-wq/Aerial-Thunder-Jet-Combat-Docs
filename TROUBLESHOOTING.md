# Troubleshooting

This guide covers known setup and runtime checks for the supplied Unreal Engine 5.7 project.

## Start With the Log

Editor and packaged builds write logs under the project's `Saved/Logs` directory. For multiplayer problems, collect the host and joined-client logs from the same short test.

Record:

- Test mode: offline, private, or public EOS
- Host and joined-player roles
- Map and selected loadout
- Approximate FPS
- The exact action that failed
- Whether the problem happened before or after respawn

## Build and Packaging

### C++ compilation fails

1. Close Unreal Editor before rebuilding plugin code.
2. Confirm the project is opened with Unreal Engine 5.7.
3. Regenerate project files if the IDE project is stale.
4. Build the editor target before packaging.
5. Read the first compiler error, not only `Unknown Error` at the end.

### Blueprint widgets report missing bindings

Several C++ widgets find optional controls by configured widget name. Confirm that the Designer names match the names set in Class Defaults.

Examples include profile region/location controls, settings controls, mission result buttons, and killer-card text widgets.

When a widget cannot use the preferred name because a Blueprint variable already owns it, use a unique Designer name and update the matching configurable name in Class Defaults.

### Packaged build opens a blank or white screen

Check:

- The target map is included in packaging/cooking.
- The configured travel map name is valid.
- The selected pawn class and spawn point are valid.
- The loading widget is not left above the viewport after travel.
- The log contains successful `OpenLevel`/travel and GameMode initialization.

Test offline, private, and public travel separately. A failure in every non-mission mode usually indicates a shared travel/loading path rather than EOS itself.

## Input and Controllers

### A changed binding is lost after restarting

- Use **Apply Settings** to activate the pending bindings, then **Save Settings** to persist them.
- Bindings are stored per local player in the `AT_GM_InputBindings` save slot; they are not replicated account or server data.
- Confirm the settings screen belongs to the correct local player and that the packaged build can write to its Saved directory.

### Moving a stick changes menu selection instead of capturing the axis

- Click the desired binding slot and wait for its short capture-arm delay before moving the stick.
- Move the intended axis decisively and release it; minor resting drift is deliberately ignored.
- If selection still moves first, check controller calibration and dead zones, then retry with the window focused.

### One controller affects two packaged game windows

Only the focused packaged window should consume gamepad input. Confirm `Slate.RequireFocusForGamepadInput=1`, click the intended window, and repeat the test. This is especially important when testing server and client on one PC.

### A PlayStation controller or HOTAS is not detected

The binding screen can capture only Unreal `FKey` values supplied by the active input backend. A PlayStation controller may require a stable USB/Bluetooth connection or a compatible platform input layer such as Steam Input. A HOTAS may require Unreal's Raw Input support, a device profile, and axis calibration. The runtime binding UI does not by itself add a missing device driver or backend mapping.

### Thunder repeatedly appears too close or directly overhead

- Use the world-centered placement mode and position the Thunder actor near the intended storm region.
- Increase both minimum and maximum horizontal distance for a wider map.
- Tune the weighted spawn profiles for left/right, near/far, and low/high coverage.
- Adjust profile scale ranges and material weights for more visual variation.
- Avoid the legacy player-relative mode when one shared multiplayer storm field is required.

## EOS and Sessions

### Public multiplayer is disabled

This is expected in the Fab-ready project until EOS is configured.

Verify:

- Online Subsystem EOS is enabled.
- Socket Subsystem EOS is enabled.
- EOS artifact values are populated.
- `DefaultArtifactName` exactly matches `ArtifactName`.
- `[OnlineSubsystemEOS] bEnabled=True`.
- `[OnlineSubsystem] DefaultPlatformService=EOS`.
- The editor was restarted.

See [EOS Setup](EOS_SETUP.md).

### UI stays on Connecting to EOS

- Finish the Account Portal login window.
- Check `LogEOS`, `LogEOSSDK`, and identity messages.
- Verify the selected sandbox and deployment.
- Do not enable public actions until the local identity reports logged in.

### Public login fails

- Recheck client credentials and artifact values.
- Confirm the two test accounts are different.
- Confirm the account is permitted in the selected EOS environment.
- Restart after changing EOS configuration.

### No public sessions are found

- Confirm host and client use the same product, sandbox, deployment, and artifact.
- Confirm the host created a public EOS session.
- Wait for the asynchronous search to complete.
- Check that both players are logged in.

### Private sessions are not found

- Confirm both clients are using the private/NULL workflow.
- Host before pressing Find on the second client.
- Verify the chosen map is available in both builds.
- Test two packaged clients on the same machine before testing separate machines.

## Multiplayer Movement and Weapons

### Remote jet shakes or jitters

Small shake can still appear during close slow passes on real internet connections.

Check:

- Both clients maintain a stable frame rate.
- The host connection has stable upload and latency.
- The test uses the same build on both machines.
- Network emulation is disabled unless intentionally testing it.
- The issue is observed in both host directions.

Do not judge remote smoothing from only one role. Swap who hosts.

### Joined player feels a small control delay

The server is authoritative, so a poor or unstable path to the host can affect joined-player presentation. Compare against a local two-client packaged test and a second cross-network run.

### Projectile or effect appears behind a fast jet

The project includes weapon-spawn corrections, but severe latency can still make rockets, missiles, or flares appear briefly behind a high-speed aircraft.

Confirm:

- Bullet spawn remains correct at high speed.
- The issue affects only remote presentation.
- Both players use matching builds.
- Logs show no rejected fire requests or invalid spawn transforms.

### Exhaust works before crash but not after respawn

- Confirm the exhaust mode is not `None`.
- Verify exhaust components rebuild during runtime refresh.
- Verify the respawned pawn uses the expected mesh and exhaust sockets.
- Test idle, full throttle, and afterburner after every respawn.

## Radar and Targeting

### AI appears friendly on radar

Confirm the AI radar signature/team classification is configured as hostile. Player jets use replicated team data; GroundTGT, AirTGT, and AI use their supported target/signature classification.

### Ground or air targets have different colors for host and client

Check that both sides resolve the same target relationship and that target actors replicate their classification. Do not derive a global target color from local authority alone.

### Auto-lock audio continues in manual mode

Manual targeting must suppress the auto-target widget and its lock audio. Confirm the targeting mode switch disables both presentation paths, not only the widget visibility.

## Audio

### AI flares or gun are audible from too far away

- Assign the AI action attenuation asset.
- Confirm the sound is spawned as a spatial sound at the AI location.
- Check the Blueprint's remote audible-distance limit.
- Confirm the cue does not contain an unattenuated 2D playback path.

### Thunder plays twice

Confirm only one thunder FX actor is active and that concurrency/cooldown prevents overlapping triggers. The thunder actor should not be duplicated per player.

### Warning phrases repeat rapidly

Review warning cooldowns and state transitions. A warning should start when its condition becomes active, remain controlled while active, and stop cleanly when the condition clears.

## Missions

### Mission starts but no radio plays

- Enable automatic playback for the configured mission audio sequence.
- Assign each beat a sound.
- Check delay-before and delay-after values.
- Confirm the MissionDirector is allowed to run for the current mission travel.

### Waypoint immediately completes the mission

Disable **Complete Mission when Final Waypoint Passed** when the mission also requires targets. Mission 03 uses the waypoint to begin combat, while configured required targets determine completion.

### Waypoint remains visible after passing

Enable the waypoint's passed visual state or hide/destroy behavior used by the MissionDirector event configuration.

### Targets are visible before the waypoint

Configure the targets as mission-activated actors and let the MissionDirector apply their initial hidden/disabled state. Avoid adding separate Event Graph wiring that fights the director.

### Action music does not start

- Assign Mission Action Music.
- Configure the waypoint event to start it.
- Verify its volume and fade-in time.
- Confirm no completion/failure/pause path immediately fades it out.

### No Level Sequence warning appears

Mission 03 intentionally supports a no-sequence intro and fade-in flow. Use the no-sequence fallback without enabling debug warnings for a deliberately empty sequence.

## AI

### AI does not attack

- Confirm Auto Activate or mission activation occurs.
- Confirm a valid hostile target exists.
- Check gun/missile enable flags and ranges.
- Check line-of-sight and aim-cone requirements.
- Confirm the selected difficulty preset is applied.

### AI becomes too easy or dies from one hit

Review the AI health component and the selected difficulty damage values. Weapon damage dealt by the AI and damage received by the AI are separate concerns.

### AI crashes in terrain

Increase avoidance look-ahead and clearance cautiously, then test high-speed pursuit through the actual terrain. The project includes avoidance sensors and escape behavior, but extreme terrain traps can still defeat AI pathing.

## UI and Profile

### Name or server field accepts too much text

Confirm the editable text control is bound to the supplied length guard. Player names use a 16-character maximum.

### Location is Unknown on the killer card

Confirm region/location were saved in the root profile and replicated into PlayerState before combat. AI location remains `Unknown` unless a project-specific AI location is supplied.

## When Reporting an Issue

Provide:

1. Reproduction steps.
2. Expected and actual behavior.
3. Editor or packaged build.
4. Single-player, private, or public EOS mode.
5. Host/client role.
6. Matching logs.
7. A short video or screenshot when the issue is visual.

## Related Documentation

- [Quick Start](QUICK_START.md)
- [EOS Setup](EOS_SETUP.md)
- [Multiplayer](MULTIPLAYER.md)
- [Mission System](MISSION_SYSTEM.md)
- [AI System](AI_SYSTEM.md)
