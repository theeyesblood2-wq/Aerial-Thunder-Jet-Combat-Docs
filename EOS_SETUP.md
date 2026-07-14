# Epic Online Services (EOS) Setup Guide

## EOS Overview

Epic Online Services (EOS) enables Aerial Thunder to support public internet multiplayer with:
- Player authentication
- Session management
- Matchmaking
- Player progression
- Social features

---

## Prerequisites

### Required Accounts & Access

1. **Epic Games Account**
   - Create at https://www.epicgames.com
   - Personal or business account
   - Free tier is sufficient

2. **EOS Developer Account**
   - Access EOS dev portal at https://dev.epicgames.com
   - Link Epic Games account
   - Accept EOS terms of service

3. **EOS Application Registration**
   - Register application in EOS dashboard
   - Note: Organization and product names

### Technical Requirements

- **Unreal Engine 5.7+** with EOS plugin enabled
- **Internet connection** — For EOS communication
- **Server infrastructure** — Dedicated server or cloud hosting
- **SSL certificate** — For secure communications (optional but recommended)

---

## Step 1: Register EOS Application

### In Epic Games Developer Portal

1. Navigate to **EOS Dev Portal** → https://dev.epicgames.com/portal/
2. Login with Epic Games credentials
3. Click **"Create New Application"**
4. Enter application details:
   - **Application Name:** "Aerial Thunder" or custom name
   - **Category:** Games
   - **Deployment:** Select region
5. Click **Create**

### Receive Credentials

After creation, note these credentials (keep secret):
- **Client ID** — Application identifier
- **Client Secret** — Authentication key
- **Organization ID** — Account organization ID
- **Product ID** — Application product ID

**⚠️ WARNING:** Do NOT share Client Secret or credentials in public repositories.

---

## Step 2: Configure UE Project

### Enable EOS Plugin

1. **Edit → Plugins**
2. Search "Online Subsystem EOS"
3. **Check "Enabled"**
4. Restart editor

### Project Settings Configuration

1. **Edit → Project Settings → Online → EOS**
2. Set the following:

#### Authentication

```
[OnlineSubsystemEOS]
bEnabled=True
CacheDir=Saved/EOS

[OnlineSubsystemEOS.Auth]
ClientId=YOUR_CLIENT_ID
ClientSecret=YOUR_CLIENT_SECRET
bUseProductUserIdCache=True
CacheExpireTime=86400
```

#### Session Management

```
[OnlineSubsystemEOS.Sessions]
bUseS2SBackend=True
SessionPort=7777
MaxPlayers=32
SessionTimeout=3600
```

#### Platform Settings

```
[OnlineSubsystemEOS.Platform]
bSandboxEnvironment=False
TickInterval=0.1
CacheDir=Saved/EOS
```

### DefaultEngine.ini Configuration

Edit **Config/DefaultEngine.ini** and add/modify:

```
[/Script/Engine.GameEngine]
+NetDriverDefinitions=(DefName="GameNetDriver",ClassName="/Script/Engine.GameNetDriver",ClientConnectionClass="/Script/Engine.NetConnection")

[OnlineSubsystemUtils.IpNetDriver GameNetDriver]
AllowClientNetTravelToMultiplayerMaps=True

[OnlineSubsystem]
DefaultPlatformService=EOS
bEnabled=True

[OnlineSubsystemEOS]
bEnabled=True

[OnlineSubsystemNull]
bEnabled=False

[OnlineSubsystemSteam]
bEnabled=False
```

---

## Step 3: Configure Dedicated Server (if applicable)

### Server Build Options

If using dedicated servers (recommended for scalability):

1. **Build project as dedicated server**
   ```
   Unreal Automation Tool BuildCook -project=AerialThunder.uproject -platform=Win64 -configuration=Shipping -cook -server -stage -pak -archive
   ```

2. **Deploy to server** (AWS, Azure, Google Cloud, etc.)

3. **Configure server parameters:**
   - Listen port (7777 default)
   - Max players
   - Map rotation
   - Session type (public/private)

### Peer-to-Peer (P2P) Alternative

For smaller deployments, use P2P:
- **Player connects directly** to host player
- **No dedicated server** required
- **Simpler setup** but limited scalability
- **Better for small player counts** (4-8 players)

**To enable P2P:**
1. Set `SessionType=P2P` in project config
2. First player acts as host
3. Others connect to host IP

---

## Step 4: Update PlayerController & GameMode

### Update PlayerController

In your player controller blueprint or C++:

```cpp
// Connect to EOS on login
void AYourPlayerController::BeginPlay()
{
    Super::BeginPlay();
    
    // Initialize EOS authentication
    IOnlineSubsystem* Subsystem = IOnlineSubsystem::Get(EOS_SUBSYSTEM);
    if (Subsystem && Subsystem->GetAuthInterface().IsValid())
    {
        Subsystem->GetAuthInterface()->Login(
            0,  // LocalUserNum
            FOnlineAccountCredentials(
                TEXT("AccountPortal"),
                TEXT(""), // Auto-login if using device auth
                TEXT("")
            )
        );
    }
}
```

### Update GameMode

Ensure GameMode handles session creation:

```cpp
// Create EOS session on game start
void AYourGameMode::PostLogin(APlayerController* NewPlayer)
{
    Super::PostLogin(NewPlayer);
    
    // Register with EOS session
    IOnlineSessionPtr SessionInterface = IOnlineSubsystem::Get(EOS_SUBSYSTEM)->GetSessionInterface();
    if (SessionInterface.IsValid())
    {
        FOnlineSessionSettings SessionSettings;
        SessionSettings.bIsDedicated = true;
        SessionSettings.NumPublicConnections = 8;
        SessionSettings.bAllowInvites = true;
        SessionSettings.bUsesPresence = true;
        
        SessionInterface->CreateSession(0, NAME_GameSession, SessionSettings);
    }
}
```

---

## Step 5: Test EOS Integration

### Local Testing

1. **Enable EOS credentials** in project settings
2. **Run project** in editor or packaged build
3. **Attempt login** to EOS
4. **Verify authentication** in EOS dashboard

### Verify Authentication

Check EOS dashboard under **Deployments → Player Logins**:
- See authenticated player accounts
- Monitor login/logout events
- Verify no authentication errors

### Test Session Creation

1. **Create session** from game menu
2. **Verify in dashboard** → Sessions list
3. **Join session** from another client
4. **Verify replication** working correctly

---

## Step 6: Deploy to Production

### Pre-Deployment Checklist

- [ ] Client ID and Secret configured (not in builds!)
- [ ] Server infrastructure deployed
- [ ] SSL certificates installed (if applicable)
- [ ] Database connections verified
- [ ] Backup systems in place
- [ ] Monitoring/logging configured
- [ ] Support team trained

### Production Deployment

1. **Build for production**
   ```
   Unreal Automation Tool BuildCook -project=AerialThunder.uproject -platform=Win64 -configuration=Shipping
   ```

2. **Deploy server builds** to hosting provider

3. **Update client builds** with production EOS configuration

4. **Verify connectivity** — Test from live build

5. **Monitor logs** — Watch for connection issues

### Production Configuration

In production config:

```
[OnlineSubsystemEOS]
bSandboxEnvironment=False  // Use production environment
bLogToConsole=True
LoggingLevel=Verbose
```

---

## Credentials Management (SECURITY)

### Best Practices

⚠️ **NEVER:**
- Commit credentials to git
- Include secrets in shipped games
- Share credentials publicly
- Use same credentials across environments

### Secure Credential Storage

**Option 1: Environment Variables**
```cpp
FString ClientId = FPlatformMisc::GetEnvironmentVariable(TEXT("EOS_CLIENT_ID"));
FString ClientSecret = FPlatformMisc::GetEnvironmentVariable(TEXT("EOS_CLIENT_SECRET"));
```

**Option 2: Secure Config Files**
- Store config on server only
- Client downloads at launch
- Config encrypted in transit

**Option 3: Backend Service**
- Game contacts backend service
- Backend provides EOS credentials
- Credentials never stored on client

**Recommended Approach:** Backend service (Option 3) is most secure for production.

---

## Common EOS Integration Tasks

### Adding Friends System

```cpp
void AYourPlayerController::AddFriend(FString FriendUserId)
{
    IOnlineSubsystem* Subsystem = IOnlineSubsystem::Get(EOS_SUBSYSTEM);
    IOnlineFriendsPtr FriendsInterface = Subsystem->GetFriendsInterface();
    
    FriendsInterface->SendInvite(
        0,  // LocalUserNum
        FriendUserId,
        FString(TEXT("Come fly with me!"))
    );
}
```

### Tracking Player Statistics

```cpp
void AYourGameMode::RecordPlayerStatistic(APlayerController* Player, int32 Kills)
{
    IOnlineSubsystem* Subsystem = IOnlineSubsystem::Get(EOS_SUBSYSTEM);
    IOnlineLeaderboardsPtr LeaderboardInterface = Subsystem->GetLeaderboardsInterface();
    
    FOnlineStatsRow StatRow;
    StatRow.SetIntStat(FName(TEXT("Kills")), Kills);
    
    LeaderboardInterface->WriteLeaderboards(nullptr, StatRow);
}
```

### Saving Cloud Data

```cpp
void AYourPlayerController::SaveProgressToCloud(FString JsonData)
{
    IOnlineSubsystem* Subsystem = IOnlineSubsystem::Get(EOS_SUBSYSTEM);
    IOnlineUserCloudPtr CloudInterface = Subsystem->GetUserCloudInterface();
    
    CloudInterface->WriteUserFile(
        0,  // LocalUserNum
        TEXT("PlayerProgress.json"),
        TArray<uint8>(reinterpret_cast<uint8*>(TCHAR_TO_ANSI(*JsonData)), JsonData.Len())
    );
}
```

---

## Troubleshooting EOS

### Authentication Fails

**Cause:** Wrong credentials, network issue, sandbox/production mismatch
**Solution:**
1. Verify Client ID and Secret in project settings
2. Check EOS dashboard — Verify application active
3. Confirm internet connection working
4. Verify sandbox/production environment match

### Sessions Not Appearing in Dashboard

**Cause:** Session not properly registered, network issue
**Solution:**
1. Check GameMode creates session (see code example above)
2. Verify session interface initialized
3. Monitor logs for errors
4. Restart application

### Player Progression Not Saving

**Cause:** Cloud save not configured, permissions issue
**Solution:**
1. Enable cloud save in project settings
2. Verify player has write permissions
3. Check cloud storage quota
4. Review leaderboard/statistics configuration

### Performance Issues with EOS

**Cause:** Tick rate too high, too many operations
**Solution:**
1. Reduce EOS tick rate: `TickInterval=0.2`
2. Batch operations when possible
3. Use async operations for I/O
4. Profile with EOS SDK profiler

---

## Monitoring & Maintenance

### EOS Dashboard Monitoring

Regular checks:
- **Active players** — Monitor concurrent player count
- **Authentication events** — Check for unusual patterns
- **Session metrics** — Average session length, churn rate
- **Error logs** — Review and address errors

### Server Logs

Monitor server-side logs for:
- Connection issues
- Authentication failures
- Session creation/destruction errors
- Network timeouts

### Player Support

Common issues to address:
- EOS login failures → Provide account recovery process
- Session join failures → Troubleshoot network connectivity
- Cloud save issues → Implement fallback data

---

## Next Steps

- **Test locally:** Run in-editor multiplayer with EOS
- **Setup dedicated servers:** Deploy server infrastructure
- **Configure matchmaking:** Set up custom matchmaking rules
- **Launch beta:** Invite players to test EOS integration
- **Go live:** Deploy to production

---

## Additional Resources

- EOS Documentation: https://docs.epicgames.com/en/web-api-ref/epic-online-services/
- Unreal EOS Plugin: UE5 Plugins → Online Subsystem EOS
- EOS Dashboard: https://dev.epicgames.com/portal/

---

**Prepare your backend. Authenticate your players. Launch online.**
