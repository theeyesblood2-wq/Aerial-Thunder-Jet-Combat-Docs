# HUD and Radar

This guide covers the cockpit HUD, tactical radar, radar signatures, target identity, and automatic/manual targeting presentation.

## Core Classes

- `AJetCockpitHUD` and `UJetCockpitHUDWidget` provide cockpit HUD presentation.
- `UJetTacticalRadarComponent` gathers and classifies radar contacts.
- `UJetRadarWidget` draws the tactical display.
- `UJetRadarSignatureComponent` identifies a jet to radar and supplies team information.
- `UJetTargetingComponent` supplies automatic target/lock state.
- `UJetManualTargetingComponent` supplies manual TAD capture and lock state.

The HUD reads gameplay state. It does not own movement, ammo, damage, or target authority.

## Cockpit HUD

The included cockpit presents flight and combat information such as:

- aircraft attitude and pitch ladder/cues
- speed and flight information
- weapon and ammunition state
- target/lock feedback
- warning feedback
- tactical radar contacts
- manual targeting/TAD output

HUD elements are configured on the aircraft and widget Blueprints. Keep display styling in UMG and keep authoritative values in the jet components.

## Tactical Radar

`UJetTacticalRadarComponent` scans for supported contacts and supplies them to `UJetRadarWidget`.

Supported project contacts include:

- other player jets
- AI jets
- `AirTGT` actors
- `GroundTGT` actors

The radar exposes Blueprint-editable scan/layout/widget settings. The widget also exposes drawing and brush options so the visual style can be replaced without changing detection logic.

## Radar Signatures and Teams

Player and AI aircraft should contain `UJetRadarSignatureComponent`.

The signature supplies the team identity used by radar classification. AI can override its signature team through `UJetAIPilotComponent`; its default AI radar team is configurable.

Contact colors represent relationship to the local player:

| Relationship | Default meaning |
|---|---|
| Friendly | Same team as the viewing player. |
| Enemy | Different team from the viewing player. |

Ground and air targets retain their configured target/team behavior. Do not classify every non-owned actor as an enemy; use the replicated team/signature data.

### AI Appears Friendly

If an enemy AI appears as a friendly contact:

1. Select the AI Blueprint's `JetAIPilotComponent`.
2. Enable the radar-signature team override if the Blueprint depends on it.
3. Assign a team different from the player team.
4. Confirm the AI jet contains a `JetRadarSignatureComponent`.
5. Test from the actual local player, not only from the server viewport.

## Automatic Target UI

Automatic targeting uses the normal forward-view target widget and lock audio.

The target widget is only presentation. Target visibility, lock validity, and missile firing permission come from `UJetTargetingComponent` and `UJetWeaponComponent`.

Default controls:

- `T`: toggle automatic targeting
- `1`: next target
- `2`: previous target

## Manual TAD Targeting

Manual targeting uses a dedicated scene-capture/TAD workflow. It is intended for cockpit use and can filter what the capture renders.

Default controls:

- `3`: enter/leave manual targeting
- `4`: toggle manual lock

When manual targeting is active:

- the automatic target widget is hidden
- automatic lock audio is suppressed
- the TAD/capture view becomes the targeting presentation
- lock and fire remain subject to the normal authoritative weapon rules

## Locked Target Widget

The locked-target widget component is used by automatic targeting. It should not remain active for manual targeting or for a target that is no longer valid.

If a lock box remains visible unexpectedly, verify:

1. automatic targeting is active
2. the target remains valid and in range
3. manual mode has not taken presentation ownership
4. the component's runtime visibility is being controlled by targeting state

Do not solve runtime visibility by permanently disabling the component in the Blueprint; that also removes valid lock feedback.

## Warnings and Awareness

The cockpit warning system includes configurable audio/state handling for conditions such as altitude/ground proximity and incoming threats. Warning playback uses cooldown/state gating to avoid repeating partial phrases every frame.

Default warning-system toggle: `K`.

## Customizing the HUD

To replace the presentation safely:

1. Create a child of the included HUD/widget class.
2. Preserve required bound widget names used by the parent C++ class.
3. Change layout, fonts, colors, brushes, and animations in UMG.
4. Read data from the jet components or exposed accessors.
5. Avoid adding gameplay authority to widget graphs.

## Performance Guidance

- Keep scene-capture resolution appropriate for the TAD's on-screen size.
- Disable or reduce manual capture work while manual targeting is inactive.
- Avoid scanning the entire world from UMG Tick.
- Let `UJetTacticalRadarComponent` own contact collection.
- Use stable widget dimensions so contact updates do not resize the layout.

## Multiplayer Checklist

- Each player sees contacts relative to their own team.
- AI is enemy/friendly according to its radar signature, not server ownership.
- `AirTGT` and `GroundTGT` contacts remain supported.
- Automatic lock UI/audio is local to the targeting player.
- Manual targeting does not leak automatic lock audio.
- HUD values survive respawn and loadout changes.

## Screenshot Placeholders

- Cockpit HUD overview
- Friendly and enemy radar contacts
- Ground and air target contacts
- Automatic target lock
- Manual TAD capture view

See also: [Weapons and Targeting](WEAPONS_AND_TARGETING.md), [Flight and Cameras](FLIGHT_AND_CAMERAS.md), and [AI System](AI_SYSTEM.md).
