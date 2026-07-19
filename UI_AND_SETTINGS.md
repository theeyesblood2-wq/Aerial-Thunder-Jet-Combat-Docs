# UI and Settings

## Overview

The project includes a complete UMG workflow for first launch, root navigation, offline setup, mission selection, multiplayer sessions, deployment, settings, pause/results, killed-in-action feedback, and loading screens. C++ base widgets use optional name bindings so designers can replace the presentation while keeping the workflow.

---

## First Launch and Profile

The startup flow supports:

1. A one-time studio/logo screen.
2. A profile screen for username, region, and location.
3. Validation and local persistence.
4. Direct root-menu entry on later launches when the profile is complete.

Username rules are enforced at input and validation time. The supplied maximum is 16 characters. Server names use the same profanity/guard-word validation path and a configurable maximum length.

Region and location are player-entered profile metadata. They are advertised in session rows and can be shown on killer information. The template does not automatically geolocate a player from an IP address.

---

## Root Menu

The root widget uses a screen switcher rather than opening a separate widget for every internal page. Included paths cover:

- Single player
- Free flight
- Mission selection
- Multiplayer selection
- Private multiplayer
- Public multiplayer
- Settings
- Aircraft, map, loadout, AI, and control selections

Screen transitions are designer-authored UMG animations assigned in Class Defaults. Internal switcher navigation can play the configured transition; flows that open a separate top-level widget can bypass it.

Mission entries are data-driven. Each entry defines its button name, mission ID, display name, map, enable/unlock state, optional prerequisite, and travel options.

---

## Offline Setup

Free Flight and Play Mission setup use configurable option arrays for:

- Aircraft class
- Loadout ID
- Map
- AI class/count/difficulty
- Control mode
- Grounded or airborne start defaults

The supplied root presents AI as `Normal` and `Advanced`. These map into the underlying AI difficulty configuration; the full internal AI component also supports additional tuning presets.

The menu passes the selected setup through travel options and the game mode applies it when the destination map starts.

---

## Multiplayer UI

Private/public session menus support:

- Player identity and team selection
- Map selection
- Server name
- Maximum players
- Host, find, select, and join actions
- Session rows showing server/map/region/location/player counts
- EOS configuration/login status for public internet sessions

Public Host/Join remain disabled until EOS is configured, initialized, and the local user is logged in. While login is active, the UI can show `Connecting to EOS...`; configuration or login failures keep public actions unavailable with a status message.

The supplied multiplayer game flow is team-based and uses listen-server sessions. It does not include ranked matchmaking, a browser-side ping meter, manual IP entry, or built-in voice chat.

---

## Deployment UI

The deployment widget uses a two-screen switcher:

- Main deployment selection
- Selected multiplayer loadout

Like the root menu, the transition animation is assigned in the widget defaults. Deployment leads into the selected jet/loadout spawn workflow.

---

## Settings Pages

`UAT_GM_SettingsPanelWidget` supports Apply, Save, Reset, category navigation, unsaved-change tracking, optional widget-name bindings, and a dedicated runtime Key Bindings page.

### Graphics

- Resolution
- Window mode
- VSync
- Frame limit
- Overall graphics quality
- View distance quality
- Shadow quality
- Effects quality
- Post-process quality

### Visual

- Brightness/gamma
- Bloom enabled
- Motion blur enabled
- Camera shake enabled
- Camera shake strength
- Lens flare enabled
- Jet exhaust FX mode

The exhaust selector supports Niagara, Static Mesh + Material, and the combined mode. Static Mesh + Material is the recommended performance baseline.

### Audio

- Music enabled
- Master volume
- Music volume
- SFX volume
- UI volume
- Engine volume
- Weapon volume

The assigned sound mix and sound classes determine which assets each slider controls.

### Controls

- Flight control mode
- Mouse sensitivity
- Controller sensitivity
- Gamepad deadzone
- Invert pitch
- Invert yaw

Control modes are Arcade, Normal, Advanced, and Realsim.

### Key Bindings

- Dynamic rows for packaged action and axis definitions
- Primary and Secondary slots
- Keyboard, mouse, gamepad button, trigger, and analog-stick capture
- Duplicate assignment protection
- Apply, Save, full Reset Bindings, and right-click single-slot reset
- Local-only persistence per player

The page is available from root Settings before gameplay. Pause-menu integration remains deferred.

### UI

- Show HUD
- Show target markers
- Show guide window

Legacy optional bindings for HUD scale/help remain for compatibility with older layouts, but they are not required by the current UI Settings workflow.

### Profile

- Current username display
- Username edit/save/reset
- Validation status

Profile region/location are collected by the startup profile workflow and stored by the same user-settings subsystem.

---

## Pause, Results, and Death Flow

The game mode supports pause/menu travel, mission result widgets, a killed-in-action countdown, respawn, and spectator presentation.

When another player or AI causes the elimination, the death flow can show:

- Killer name
- Aircraft display name
- Loadout
- Flight/control model
- AI difficulty where applicable
- Location metadata

Unknown or non-applicable fields remain visible with an `Unknown` value so Blueprint-designed rows and borders keep a stable layout. A world spectator camera can observe the killer during the respawn countdown; self-elimination does not require killer spectating.

---

## Widget Binding Pattern

Many base widgets support two approaches:

1. Keep the documented default widget names.
2. Give widgets custom names and assign those names in the Blueprint Class Defaults binding structure.

The second approach is useful when an inherited C++ property already uses a desired name. Renaming a UMG widget is safe when the corresponding Class Defaults binding is updated to match.

Optional widgets may be omitted without breaking unrelated features. Required workflow controls should be tested after every rename.

---

## Saving and Applying

Settings and profile data are stored locally through `UAT_GM_UserSettingsSubsystem`. Use:

- Apply to update runtime behavior.
- Save to persist the current values.
- Reset to restore the configured defaults.

The subsystem applies game-user settings, visual console settings, input settings, UI visibility, brightness overlay, volume classes, and the stored control mode.

See also:

- [Quick Start](QUICK_START.md)
- [Inputs](INPUTS.md)
- [EOS Setup](EOS_SETUP.md)
- [Settings Reference](SETTINGS_REFERENCE.md)
