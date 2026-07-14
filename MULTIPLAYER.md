# Multiplayer Guide

## Multiplayer Overview

Aerial Thunder supports three multiplayer modes:
1. **Local Editor Multiplayer** — Multiple players in editor (testing)
2. **Private LAN Multiplayer** — Multiple instances on same network
3. **Public EOS Multiplayer** — Internet multiplayer via Epic Online Services

---

## Local Editor Multiplayer

### Quick Setup

1. **Open multiplayer map** — e.g., `DogfightArena`
2. **Edit → Project Settings → Engine → Play**
3. **Set "Net Mode"** to "Play as Listen Server"
4. **Set "Number of Players"** to 2, 3, or 4
5. **Click Play**

### Editor Multiplayer Features

- **Multiple viewports** — Each player has separate window
- **Replicated gameplay** — Actions sync across all clients
- **Server authoritative** — First player is server
- **Perfect for testing** — Verify multiplayer logic locally
- **No network lag** — Instant feedback (unrealistic but useful for testing)

### Limitations

- **Local only** — Can't play with remote players
- **Single PC only** — All players run on same computer
- **Performance** — Can be CPU intensive for 4+ players
- **Not realistic** — No network lag simulation

---

## Private LAN Multiplayer

### Setup for LAN Play

#### Build the Project

1. **File → Package Project → Windows (64-bit)**
2. Choose output directory
3. Wait for build to complete (10-20 minutes)

#### Run Server

1. Run the executable with parameter: `-server`
2. Game starts in server mode (background, no viewport)
3. Server listens on default port (7777)

#### Run Clients

1. Run multiple instances of the executable (normal mode)
2. Each player selects "Join Game"
3. Prompt for server IP address
4. Enter server IP (e.g., "192.168.1.100")
5. Players connect and spawn in game

### LAN Multiplayer Features

- **Full replication** — All gameplay replicated across network
- **Server authoritative** — Server controls all game logic
- **Listen server** — Server can also be a player
- **Lag simulation** — Network latency affects gameplay (realistic)
- **Customizable maps** — Any multiplayer map can be hosted

### Server Configuration

**Server startup command line:**
```
AerialThunder.exe -server -log
```

**Additional parameters:**
- `-game` — Specify map (default: MainMenu)
- `-port=7777` — Specify port
- `-numplayers=4` — Max players
- `-dedicated` — Dedicated server (no player viewport)

### Connecting as Client

**Command line:**
```
AerialThunder.exe 192.168.1.100:7777
```

Or use in-game menu:
1. Main Menu → Multiplayer → Join LAN Game
2. Enter IP and port
3. Click Join

---

## Public Multiplayer (EOS)

### Epic Online Services Overview

Aerial Thunder integrates Epic Online Services (EOS) for:
- **Player accounts** — Authentication and identity
- **Sessions** — Matchmaking and lobby management
- **Progression** — Cross-platform player progression
- **Friends** — Social features and party system
- **Achievements** — Cloud-based achievement tracking

### Prerequisites for EOS

1. **Epic Games account** — Personal account at epicgames.com
2. **EOS Application** — Register application in EOS dashboard
3. **EOS credentials** — Client ID and Client Secret
4. **Project configuration** — Add credentials to UE project
5. **Backend setup** — Deploy dedicated servers or configure peer-to-peer

### EOS Configuration

See [EOS Setup](EOS_SETUP.md) for detailed setup instructions.

---

## Game Modes

### Deathmatch (Free-For-All)

**Setup:**
- 2-8 players
- No teams
- Unlimited respawns
- Time limit: 15 minutes

**Objectives:**
- Eliminate as many opponents as possible
- Highest score wins
- Scoring: +1 point per kill; -1 point per death

**Strategy:**
- Maintain energy advantage
- Build distance between fights
- Use terrain for concealment
- Coordinate with no one (every player for themselves)

### Team Deathmatch

**Setup:**
- 2-8 players (divided into 2-4 teams)
- Teams compete
- Unlimited respawns
- Time limit: 20 minutes

**Objectives:**
- Eliminate opposing team members
- Highest team score wins
- Scoring: +1 point per kill; team bonus for squad wipes

**Strategy:**
- Coordinate with teammates
- Watch teammates' six
- Focus fire on single opponents
- Defend base area

### Capture The Flag (CTF)

**Setup:**
- 4-8 players (2 teams)
- Each team defends flag
- Limited respawns
- Time limit: 25 minutes

**Objectives:**
1. Steal enemy flag from their base
2. Carry flag to your base
3. Defend your flag from capture
4. First team to 3 captures wins (or highest at time limit)

**Strategy:**
- Coordinate flag defense
- Plan flag runs
- Establish air superiority over bases
- Communicate flag locations

### King of the Hill (KotH)

**Setup:**
- 4-6 players (teams or FFA)
- Designated airspace is "hill"
- Unlimited respawns
- Time limit: 20 minutes

**Objectives:**
- Control designated airspace
- Maintain presence in hill for scoring
- Eliminate threats from hill
- Highest control time wins

**Strategy:**
- Gain altitude advantage
- Use superior energy position
- Coordinate with teammates for mutual defense
- Take shifts maintaining control

---

## Ranking & Progression

### Player Rank System

**Ranks (0-50):**
- Rank 0-5: Recruit
- Rank 6-15: Cadet
- Rank 16-25: Pilot
- Rank 26-35: Captain
- Rank 36-45: Colonel
- Rank 46-50: Ace

### Experience Points (XP)

XP earned from:
- **Eliminating opponent** — +100 XP per kill
- **Mission completion** — +500 XP per mission
- **Game mode bonus** — +50 XP per game mode played
- **Team victory** — +200 XP bonus
- **Match duration** — +5 XP per minute played

### Skill Rating (SR)

Competitive ranking separate from level:
- **Matches played** — Minimum 10 matches to establish rating
- **Win/loss ratio** — Primary factor
- **Elimination ratio** — K/D ratio factored
- **Team contribution** — Objective play weighted
- **Skill brackets:**
  - 0-1000: Beginner
  - 1000-2000: Intermediate
  - 2000-3000: Advanced
  - 3000-4000: Expert
  - 4000+: Legendary

---

## Multiplayer Rules & Settings

### Session Settings

**Host can configure:**
- **Player limit** — 2-8 players
- **Time limit** — 10-60 minutes
- **Score limit** — Optional (game ends at score or time)
- **Friendly fire** — On/Off (default: Off)
- **Respawn timer** — 5-30 seconds
- **Loadout switching** — Allowed/Disabled

### Anti-Cheat System

- **Fair play monitoring** — Unusual player behavior flagged
- **Damage validation** — Server validates all damage
- **Movement validation** — Impossible moves rejected
- **Network timing** — Latency outliers investigated
- **Reporting system** — Players can report suspicious activity

### Penalties

- **Team killing** — Loss of points/score
- **Excessive teamkilling** — Temporary ban from mode
- **AFK (Away from keyboard)** — Auto-kick after 5 minutes
- **Disconnect** — Replaced by bot; player can rejoin
- **Cheating suspected** — Account flagged; investigation

---

## Multiplayer HUD

### Additional HUD Elements

**Team display:**
- Teammate callsigns and status
- Teammate health/damage state
- Teammate positions on minimap

**Score display:**
- Current team score vs. opponent
- Individual player score
- Kill/death ratio
- Objective progress (CTF, KotH)

**Minimap:**
- Friendly positions (blue)
- Enemy radar contacts (red)
- Objectives/flags (objective-dependent)
- Terrain outline

**Scoreboard (Tab key):**
- All player names and scores
- K/D ratio
- Ping (latency) to server
- Team assignment

---

## Network Architecture

### Server Authority

- **All game decisions** made on server
- **Client sends input** — Player inputs sent to server
- **Server processes** — Damage, eliminations, scoring
- **Server replicates** — Updated state sent to all clients
- **Latency compensation** — Prediction smooths client-side movement

### Replication Priority

**High priority (frequent updates):**
- Player aircraft position
- Player health state
- Active threats (incoming missiles)

**Medium priority (regular updates):**
- Radar contacts
- Teammate positions
- Weapon loadout state

**Low priority (periodic updates):**
- Score updates
- Teammate status messages
- Environmental state

### Latency Handling

- **Client prediction** — Clients predict own aircraft movement
- **Server authority** — Server validates all critical actions
- **Lag compensation** — Server accounts for network delay
- **Acceptable latency** — 0-150 ms optimal; 150-300 ms playable

---

## Multiplayer Tips

1. **Communicate with team** — Use voice chat or quick messages
2. **Call out targets** — Let teammates know what you're engaging
3. **Watch your six** — Keep aware of teammate positions
4. **Share radar data** — Report aircraft and air defense positions
5. **Focus fire** — Team focus fire on single opponent wins fights
6. **Defend together** — Mutual support improves survival
7. **Use map knowledge** — Learn terrain for ambush positions
8. **Manage loadout** — Choose weapons appropriate for mode
9. **Respect skill levels** — Adjust tactics for opponent ability
10. **Have fun** — Competitive or casual, enjoy the experience

---

## Troubleshooting Multiplayer

### Can't Connect to Server

**Cause:** Server offline, wrong IP, firewall blocking
**Solution:**
1. Verify server is running
2. Confirm IP address and port
3. Check firewall allows connection
4. Try "localhost:7777" for local connections

### Lag/Latency Issues

**Cause:** High network latency or packet loss
**Solution:**
1. Check internet connection speed (minimum 5 Mbps recommended)
2. Close other bandwidth-heavy applications
3. Move closer to router
4. Try different server with lower ping
5. Restart game/router

### Disconnects During Game

**Cause:** Network interruption or server crash
**Solution:**
1. Verify internet connection stable
2. Check server status
3. Rejoin session if still active
4. Report persistent crashes to developers

### EOS Login Fails

**Cause:** Wrong credentials, network issue, EOS misconfiguration
**Solution:**
1. Verify Epic Games account credentials
2. Check internet connection
3. Review EOS setup configuration
4. See [EOS Setup](EOS_SETUP.md) for detailed troubleshooting

---

## Next Steps

- **Setup EOS:** [EOS Setup](EOS_SETUP.md)
- **Join games:** Use in-game Multiplayer menu
- **Create custom games:** Host server and configure settings
- **Compete:** Join ranked matches and climb skill ladder

---

**Squad up. Lock and load. Go online.**
