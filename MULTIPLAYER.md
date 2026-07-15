# Multiplayer

Aerial Thunder includes server-authoritative jet combat for local editor testing, private sessions, and public internet sessions through Epic Online Services (EOS).

> AT_GM and Jet_C_MT remain separate plugins. AT_GM owns the game/session flow. Jet_C_MT owns the jet, flight, weapons, FX, and replication used by the aircraft.

## Supported Workflows

| Workflow | Online subsystem | Server type | Intended use |
|---|---|---|---|
| Multiplayer PIE | Editor configuration | Listen server | Fast local development |
| Private multiplayer | NULL | Listen server | Local/private testing |
| Public multiplayer | EOS | Listen server | Internet play across networks |

The supplied project does not include a dedicated-server deployment workflow, direct-IP browser, ranked matchmaking, voice chat, or external anti-cheat integration.

## Private Multiplayer

Private multiplayer is available without EOS credentials. It uses the NULL subsystem and a listen-server session.

### Host

1. Open the private multiplayer screen.
2. Select the player team.
3. Select the map.
4. Choose the maximum player count.
5. Enter a valid server name.
6. Press **Host**.

### Join

1. Open the private multiplayer screen.
2. Select the player team.
3. Press **Find**.
4. Select a session result.
5. Press **Join**.

Session rows can display the server name, map, host region, host location, current players, and maximum players.

## Public EOS Multiplayer

Public multiplayer uses EOS Sessions V2. It is intentionally unavailable in the Fab-ready template until EOS is configured and the local player completes login.

The public screen distinguishes these states:

| State | Result |
|---|---|
| EOS is not configured | Public Host/Join stay disabled and setup guidance is shown |
| EOS is connecting | The UI reports that EOS login is in progress |
| EOS login failed | Public actions stay disabled and the UI reports the failure |
| EOS is initialized and logged in | Public Host/Find/Join become available |

See [EOS Setup](EOS_SETUP.md) for the complete configuration procedure.

## Player Profile Data

The root menu stores the player's display name, region, and location. In multiplayer, the authoritative PlayerState replicates:

- Team
- Kill count
- Death count
- Alive state
- Player region
- Player location

The same profile data is used by session results and the killed-in-action killer card. AI difficulty is shown for AI eliminations; it remains `Unknown` for human players because it is not a multiplayer player attribute.

## Team Deathmatch Flow

The supplied multiplayer game flow includes:

- Team A, Team B, and optional automatic team selection
- Server-authoritative kills and deaths
- Alive/inactive player state
- Team score and match timer presentation
- Elimination feedback and suicide feedback
- Killed-in-action countdown
- Respawn
- Killer information card
- Temporary spectating/world camera behavior

The template does not ship CTF, King of the Hill, free-for-all, progression ranks, XP, or skill rating.

## Authority and Replication

The server owns gameplay truth. Clients request actions and receive authoritative results for:

- Pawn spawn and respawn
- Jet movement state
- Weapon firing and projectile state
- Damage, destruction, kills, and deaths
- Team and player-state data
- Ground and air target state
- Multiplayer radar relationships

Cosmetic presentation is kept local where appropriate. For example, hit feedback intended only for the shooter should not become globally repeated audio.

## Network Smoothing

The jet movement system includes multiplayer smoothing for remote aircraft. Local and cross-country testing has shown generally clean own-jet movement and usable remote movement.

Real internet conditions can still produce:

- Small remote-jet shake during close, slow passes
- Brief input or action presentation delay for a joined player
- Delayed remote flares, rockets, or missiles
- Short projectile-origin corrections under poor latency

These effects depend on latency, packet timing, frame rate, and the host connection. Test both directions because a host and a joined player observe different network paths.

## Recommended Test Matrix

### Local packaged test

1. Start two packaged clients.
2. Host a private session.
3. Join from the second client.
4. Test normal and high-speed flight.
5. Perform slow close passes.
6. Fire every weapon and deploy flares.
7. Crash both players and verify respawn.
8. Verify exhaust after respawn.
9. Verify kills, suicide feedback, killer card, and scores.

### Public EOS test

1. Use two machines on different networks.
2. Host publicly and join through EOS.
3. Repeat the movement and combat checks.
4. Swap host and joined-player roles.
5. Keep the run short when collecting diagnostic logs.

## Logs

Runtime logs are written under the packaged project's `Saved/Logs` directory. Capture the host and joined-client logs from the same test run.

Useful evidence includes:

- Who hosted and who joined
- Approximate FPS for both players
- Connection conditions
- Exact moment a delay or shake occurred
- Which weapon or respawn cycle was active

## Related Documentation

- [EOS Setup](EOS_SETUP.md)
- [Weapons and Targeting](WEAPONS_AND_TARGETING.md)
- [HUD and Radar](HUD_AND_RADAR.md)
- [Troubleshooting](TROUBLESHOOTING.md)
- [Architecture](ARCHITECTURE.md)
