# Microsoft Authentication

GushenCL / MoyiCL use the official Microsoft identity platform OAuth 2.0
**Device Code Flow** to authenticate users who own Minecraft: Java Edition.

## Flow

1. The launcher requests a device code from:

   ```text
   https://login.microsoftonline.com/consumers/oauth2/v2.0/devicecode
   ```

   with the public scopes:

   ```text
   XboxLive.signin offline_access
   ```

2. The user opens `https://microsoft.com/devicelogin` in a browser and enters
   the displayed code.

3. The launcher polls:

   ```text
   https://login.microsoftonline.com/consumers/oauth2/v2.0/token
   ```

4. After Microsoft authorization, the launcher performs the standard:

   - Xbox Live user authentication;
   - XSTS authorization;
   - Minecraft Services `POST /authentication/login_with_xbox`;
   - Minecraft Services `GET /minecraft/profile`.

5. Only after Minecraft confirms ownership does the launcher create a
   Microsoft profile and launch the game.

## Security properties

- No Microsoft password is collected or stored.
- No client secret is used; this is a public client application.
- The launcher has no server-side account database and does not receive tokens.
- Access and refresh tokens are stored only in the local data directory.
- The launcher does not distribute Minecraft assets.
- The launcher does not bypass Minecraft ownership checks.

## Client ID allowlisting

Minecraft Services requires third-party application Client IDs to be reviewed
and allowlisted. Without approval, `/authentication/login_with_xbox` returns:

```text
HTTP 403 Invalid app registration
```

The project has prepared the official Java Edition Game Service API review
materials. The Client ID used by the public build is submitted for review; the
launcher reports the exact server error if approval is not yet active.

## Official references

- [Microsoft identity platform device code flow](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-device-code)
- [Register an application in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app)
- [Java Edition Game Service API review](https://help.minecraft.net/hc/en-us/articles/16254801392141)
