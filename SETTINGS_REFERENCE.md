# Settings Reference

## Configuration Files

Aerial Thunder uses multiple configuration files to manage settings. All settings can be modified via in-game menus or by editing configuration files directly.

---

## DefaultEngine.ini

**Location:** `Project/Config/DefaultEngine.ini`

Core engine settings:

```
[/Script/Engine.Engine]
bUseFixedFrameRate=False
FixedFrameRate=60

[/Script/Engine.PlayerController]
bShowMouseCursor=False
DefaultInputComponentClass=/Script/EnhancedInput.EnhancedPlayerInput

[/Script/Engine.GameEngine]
GameEngine=AerialThunderGameEngine

[OnlineSubsystem]
DefaultPlatformService=EOS
```

---

## DefaultGameUserSettings.ini

**Location:** `Project/Saved/Config/Windows/DefaultGameUserSettings.ini`

User-specific graphics and gameplay settings:

```
[/Script/Engine.GameUserSettings]
FullscreenMode=2
ResolutionSizeX=1920
ResolutionSizeY=1080
ResolutionSizeX=1920
LastUserConfirmedResolutionSizeX=1920
LastUserConfirmedResolutionSizeY=1080
LastRecommendedFullscreenMode=2
LastConfirmedFullscreenMode=2
PreferredFullscreenMode=2
Version=5
AudioQualityLevel=2
FrameRateLimit=60.000000
DesiredScreenWidth=1920
DesiredScreenHeight=1080
LastScreenWidth=1920
LastScreenHeight=1080
LastFullscreenMode=2
```

### Modifiable Settings

| Setting | Type | Range | Default |
|---------|------|-------|---------|
| `FullscreenMode` | Int | 0=Windowed, 1=Fullscreen, 2=Borderless | 2 |
| `ResolutionSizeX` | Int | Screen pixels (horizontal) | 1920 |
| `ResolutionSizeY` | Int | Screen pixels (vertical) | 1080 |
| `FrameRateLimit` | Float | 30-240 or 0 for unlimited | 60 |
| `ShadowQuality` | Int | 0=Low, 1=Medium, 2=High, 3=Ultra | 2 |
| `TextureQuality` | Int | 0=Low, 1=Medium, 2=High, 3=Ultra | 2 |
| `EffectsQuality` | Int | 0=Low, 1=Medium, 2=High, 3=Ultra | 2 |
| `AudioQualityLevel` | Int | 0=Low, 1=Medium, 2=High | 2 |

---

## Flight Configuration

**Section:** `[/Script/JetCombatMultiplayerTemplate.AirCraftPawn]`

Flight mechanics configuration:

### Arcade Mode Settings

```
[ArcadeFlightSettings]
PitchResponseMultiplier=2.0
RollResponseMultiplier=2.0
YawResponseMultiplier=1.5
ThrottleResponseTime=0.1
AutoLevelStrength=1.0
StallRecoveryAssist=1.0
AltitudeMinimumForStall=500.0
```

### Advanced Mode Settings

```
[AdvancedFlightSettings]
PitchResponseMultiplier=1.0
RollResponseMultiplier=1.0
YawResponseMultiplier=1.0
ThrottleResponseTime=2.5
AutoLevelStrength=0.5
StallRecoveryAssist=0.0
AltitudeMinimumForStall=0.0
GForceBlackoutThreshold=9.0
```

### Aircraft Performance Parameters

```
[AircraftPerformance]
MaxSpeed=550.0
CruiseSpeed=400.0
MinimumSafeAirspeed=90.0
StallSpeed=80.0
MaxAltitude=35000.0
ServiceCeiling=40000.0
FuelCapacity=8000.0
FuelBurnRateCruise=100.0
FuelBurnRateFull=300.0
EngineSpoolUpTime=5.0
EngineSpoolDownTime=10.0
MaxEngineTemperature=100.0
```

---

## Weapon Configuration

**Section:** `[/Script/JetCombatMultiplayerTemplate.WeaponSystem]`

Weapon properties and balance:

### Gun Settings

```
[GunSettings]
Ammo=Unlimited
Damage=25.0
FireRate=1200.0
EffectiveRange=3000.0
OptimalRange=500.0
Accuracy=0.95
OverheatThreshold=500
OverheatCooldownTime=10.0
Convergence=500.0
```

### Rocket Settings

```
[RocketSettings]
Ammo=8
Damage=100.0
BlastRadius=50.0
FlightSpeed=700.0
MaxRange=5000.0
Reload=0.5
MaxAmmoPerLoadout=16
```

### Missile Settings

```
[MissileSettings]
Ammo=4
Damage=150.0
MaxRange=20000.0
LockOnTime=2.5
GuidanceAccuracy=0.98
MaxG=8.0
Reload=3.0
MaxAmmoPerLoadout=8
```

### Flare Settings

```
[FlareSettings]
Ammo=32
DeployRate=10.0
EffectiveRange=200.0
EvadeChance=0.85
MaxAmmoPerLoadout=64
CooldownTime=0.5
```

---

## Camera Configuration

**Section:** `[/Script/JetCombatMultiplayerTemplate.CameraSystem]`

Camera system parameters:

```
[CameraSettings]
CockpitFOV=100.0
ShoulderFOV=80.0
ChaseFOV=60.0
ZoomSensitivity=2.0
LookSensitivity=1.5
CameraSmoothing=0.8
CameraTransitionSpeed=0.5
ShoulderDistance=50.0
ChaseDistance=200.0
```

---

## Audio Configuration

**Section:** `[/Script/Engine.AudioSettings]`

Audio system settings:

```
[AudioSettings]
MasterVolume=0.8
EngineVolume=0.7
WeaponVolume=0.75
RadioVolume=0.8
WarningVolume=0.9
MusicVolume=0.6
AmbienceVolume=0.5
EnableDynamicMusic=True
MusicIntensity=1.0
EnableSurroundSound=True
EnableReverb=True
```

---

## Multiplayer Configuration

**Section:** `[/Script/Engine.GameNetworkManager]`

Network and multiplayer settings:

```
[MultiplayerSettings]
MaxPlayers=8
ListenServerPort=7777
ConnectionTimeout=120
Ping_Max=500
Ping_Optimal=100
ReplicationUpdateRate=10
NetServerMaxTickRate=100
NetClientTicksPerSecond=60
EnableVoiceChat=True
VoiceChatCodec=Opus
```

---

## HUD Configuration

**Section:** `[/Script/Engine.HUD]`

HUD display settings:

```
[HUDSettings]
HUDScale=1.0
HUDOpacity=1.0
MinimalHUDMode=False
ShowCrosshair=True
ShowSpeedometer=True
ShowAltimeter=True
ShowCompass=True
ShowWeaponStatus=True
ShowRadar=True
ShowObjectives=True
ShowWarnings=True
```

---

## Difficulty Configuration

**Section:** `[/Script/Aerial Thunder GameMode]`

AI difficulty and game balance:

```
[DifficultySettings]

[NormalDifficulty]
AIAccuracy=0.45
AIReactionTime=1.5
EnemyMultiplier=1.0
HealthMultiplier=1.0
FuelAbundance=1.5
TimeMultiplier=1.5
AutoLevelAssist=True
AimAssist=True

[AdvancedDifficulty]
AIAccuracy=0.65
AIReactionTime=0.75
EnemyMultiplier=1.5
HealthMultiplier=1.0
FuelAbundance=1.0
TimeMultiplier=1.0
AutoLevelAssist=False
AimAssist=True

[AceDifficulty]
AIAccuracy=0.85
AIReactionTime=0.25
EnemyMultiplier=2.0
HealthMultiplier=0.75
FuelAbundance=0.8
TimeMultiplier=0.75
AutoLevelAssist=False
AimAssist=False
```

---

## Graphics Configuration

**Section:** `[/Script/Engine.RendererSettings]`

Graphics and visual settings:

```
[GraphicsSettings]

[LowQuality]
ResolutionScale=0.75
FrameRate=60
ShadowQuality=0
TextureQuality=0
EffectsQuality=1
ReflectionQuality=0

[MediumQuality]
ResolutionScale=1.0
FrameRate=60
ShadowQuality=1
TextureQuality=1
EffectsQuality=2
ReflectionQuality=1

[HighQuality]
ResolutionScale=1.33
FrameRate=60
ShadowQuality=2
TextureQuality=2
EffectsQuality=3
ReflectionQuality=2

[UltraQuality]
ResolutionScale=2.0
FrameRate=60
ShadowQuality=3
TextureQuality=3
EffectsQuality=3
ReflectionQuality=3
RayTracing=True
```

---

## Control Configuration

**Section:** `[/Script/EnhancedInput.EnhancedPlayerInput]`

Control mapping defaults:

### Keyboard Defaults

```
[KeyboardDefaults]
W=Pitch Up
S=Pitch Down
A=Roll Left
D=Roll Right
Q=Yaw Left
E=Yaw Right
LeftShift=Throttle Up
LeftCtrl=Throttle Down
Space=Brake / Air Brake
Enter=Start Engine
G=Landing Gear
H=Auto Level
V=Change Camera
5=Camera Reset
LeftMouse=Fire Gun
RightMouse=Fire Rockets
MiddleMouse=Fire Missile
X=Deploy Flares
T=Auto Targeting
1=Next Target
2=Previous Target
3=Manual Targeting
4=Manual Target Lock
K=Warning System
Escape=Pause
P=Pause
Tab=Scoreboard
U=Multiplayer Dashboard
```

### Sensitivity Defaults

```
[SensitivityDefaults]
MouseSensitivity=1.0
LookSensitivity=1.0
ThrottleSensitivity=1.0
YawSensitivity=1.0
DeadZone=0.15
InvertPitch=False
InvertYaw=False
InvertCamera=False
```

---

## Performance Tuning

### CPU-Intensive Settings

Reduce for better CPU performance:
- `EnemyAICount` — Fewer AI fighters
- `PhysicsTickRate` — Lower physics simulation rate
- `ReplicationUpdateRate` — Less frequent network updates
- `ParticleQuality` — Fewer particles on screen

### GPU-Intensive Settings

Reduce for better GPU performance:
- `ShadowQuality` — Lower shadow resolution
- `TextureQuality` — Lower texture resolution
- `EffectsQuality` — Fewer particle effects
- `ReflectionQuality` — Simpler reflections

### Memory-Intensive Settings

Reduce to lower RAM usage:
- `TextureStreamingPoolSize` — Reduce streaming memory
- `CacheSize` — Smaller memory caches
- `MaxPlayers` — Fewer concurrent players

---

## Network Optimization

### Bandwidth Reduction

```
[NetworkOptimization]
ReducedNetworkQuality=False
CompressNetworkData=True
MaxPayloadSize=1024
OptimizeReplication=True
UpdateFrequency=10
```

### Latency Compensation

```
[LatencyCompensation]
ClientPrediction=True
ServerReconciliation=True
InterpolationDelay=100
ExtrapolationTime=50
```

---

## Troubleshooting Configuration

### Reset to Defaults

To reset all settings to defaults:

1. Delete `Project/Saved/Config/` directory
2. Restart game
3. Game regenerates default configuration

### Verify Configuration

Check configuration integrity:
1. Load game normally
2. Settings → [Category] → Check values
3. Modify one setting, close/reopen
4. Verify change persisted

### Common Configuration Issues

**Game won't start:**
- Check `DefaultEngine.ini` for syntax errors
- Verify all required sections present
- Restore default config

**Graphics too slow:**
- Lower quality settings in `GameUserSettings.ini`
- Reduce resolution and frame rate
- Disable expensive features (ray tracing, high effects)

**Audio not working:**
- Verify audio settings in `AudioSettings`
- Check OS audio device
- Restore default audio config

---

## Advanced Configuration

### Custom Game Modes

Add new game mode config:

```
[/Script/YourGameMode]
TimeLimitMinutes=30
ScoreLimit=50
MaxPlayersPerTeam=4
FriendlyFire=False
RespawnTime=10
```

### Server Customization

Configure dedicated server:

```
[/Script/Engine.Engine]
bUseFixedFrameRate=True
FixedFrameRate=100

[/Script/Engine.NetDriver]
AllowClientNetTravelToMultiplayerMaps=True
NetServerMaxTickRate=100
```

### Client Optimization

Optimize client settings:

```
[/Script/Engine.PlayerController]
DefaultInputComponentClass=/Script/EnhancedInput.EnhancedPlayerInput
bShowMouseCursor=False

[/Script/Engine.Pawn]
bUseControllerRotationPitch=False
bUseControllerRotationYaw=False
bUseControllerRotationRoll=False
```

---

## Next Steps

- **Edit configuration files:** `Project/Config/` directory
- **Customize game:** Modify ini files for your preferences
- **Optimize performance:** Tune settings for your hardware
- **Share configurations:** Save custom ini files for backup

---

**Tune your settings. Optimize your experience. Master your configuration.**
