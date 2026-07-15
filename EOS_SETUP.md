# Epic Online Services Setup

The Fab-ready Aerial Thunder template ships with EOS credentials intentionally blank and public EOS multiplayer disabled. Offline gameplay, missions, editor multiplayer, and private NULL-subsystem sessions remain usable before EOS is configured.

Public multiplayer becomes available only after EOS is configured, initialized, and logged in.

## Before You Begin

You need an Epic developer account and an EOS product configuration containing the values required by Unreal Engine:

- Product ID
- Sandbox ID
- Deployment ID
- Client ID
- Client Secret
- Client Encryption Key
- Artifact Name

Epic may update the Developer Portal layout. Use the current EOS portal labels that correspond to these Unreal Engine artifact fields.

## 1. Enable the Unreal Plugins

In **Edit > Plugins**, enable:

- Online Subsystem EOS
- Socket Subsystem EOS

Restart the editor after changing plugin state.

## 2. Configure the EOS Artifact

Open **Project Settings** and locate the EOS settings. Enter the product, sandbox, deployment, client, and encryption values for your EOS artifact.

Set:

- `ArtifactName` to your chosen artifact name.
- `DefaultArtifactName` to exactly the same value, including capitalization.

An empty or mismatched default artifact prevents the public workflow from becoming ready.

## 3. Enable EOS in DefaultEngine.ini

Set the active online subsystem to EOS:

```ini
[OnlineSubsystemEOS]
bEnabled=True

[OnlineSubsystem]
DefaultPlatformService=EOS
```

Keep the project net-driver definition that selects the EOS socket driver with the Unreal IP driver as fallback:

```ini
[/Script/Engine.Engine]
!NetDriverDefinitions=ClearArray
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="/Script/SocketSubsystemEOS.NetDriverEOSBase",DriverClassNameFallback="/Script/OnlineSubsystemUtils.IpNetDriver")
```

The distributed template may contain disabled or blank placeholder values. Replace them with valid values; do not treat placeholder spelling as a valid EOS configuration.

## 4. Restart and Log In

Restart the editor after configuration. Open the public multiplayer screen.

Expected flow:

1. The UI reports that it is connecting to EOS.
2. EOS Account Portal login opens when authentication is required.
3. Complete the Epic login flow.
4. Public Host/Find/Join become available after login succeeds.

Where the platform can restore the login session, later launches can continue without asking the player to repeat the full login flow.

## 5. Test a Public Session

Use packaged development builds on two machines whenever possible.

1. Confirm both builds use the same EOS product, sandbox, deployment, and artifact.
2. Sign in with different Epic accounts.
3. Host a public room on the first machine.
4. Find and join it on the second machine.
5. Verify the advertised server name, map, region, location, and player count.
6. Test gameplay and then swap host roles.

## Readiness Checks

The public UI does not rely only on `bEnabled`. It also checks whether:

- EOS is the selected public subsystem.
- EOS initialized successfully.
- A usable artifact is configured.
- Login is no longer processing.
- The local identity is logged in.

This prevents public buttons from launching broken requests before setup is complete.

## Common Problems

### Public buttons remain disabled

Check all of the following:

- Both EOS plugins are enabled.
- `bEnabled=True` is spelled correctly.
- `DefaultPlatformService=EOS` is present.
- Artifact fields are not blank.
- `DefaultArtifactName` exactly matches `ArtifactName`.
- The editor was restarted after configuration.

### EOS login fails

- Verify the client credentials and deployment.
- Confirm the Epic account is allowed to use the selected product environment.
- Review the runtime log for `LogEOS`, `LogEOSSDK`, and identity messages.
- Keep public actions disabled until login succeeds.

### Host succeeds but the other player finds nothing

- Confirm both clients use the same artifact and deployment.
- Confirm both players completed login.
- Confirm the host created a public EOS session, not a private NULL session.
- Wait for the search operation to finish before pressing Join.

### Private multiplayer stopped working

Private sessions use the NULL subsystem path. Public EOS readiness should not be used to block private editor/local testing.

## Security Notes

- Never publish your real EOS credentials in public documentation, screenshots, or a public source repository.
- The Fab template should continue to ship with blank project-specific identifiers.
- Buyers must create and configure their own EOS product.

## Scope

The supplied EOS integration covers public listen-server sessions and Account Portal login. It does not document or promise dedicated servers, EOS voice, friends, stats, achievements, cloud saves, or Steam integration.

## Related Documentation

- [Multiplayer](MULTIPLAYER.md)
- [Quick Start](QUICK_START.md)
- [Troubleshooting](TROUBLESHOOTING.md)
- [Architecture](ARCHITECTURE.md)
