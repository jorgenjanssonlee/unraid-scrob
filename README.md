# Unraid templates for Scrob

Community-maintained [Unraid](https://unraid.net/) Docker templates for [Scrob](https://github.com/ellite/scrob) — self-hosted media tracking for Jellyfin, Plex, and Emby.

**This repository is not affiliated with the Scrob author.** It packages the official `bellamy/scrob` Docker images for Unraid users. Template install and Unraid-specific setup questions belong here; application bugs and feature requests go to [ellite/scrob](https://github.com/ellite/scrob/issues).

## Templates

| Template                                             | Image                          | Description                                   |
| ---------------------------------------------------- | ------------------------------ | --------------------------------------------- |
| [scrob-omnibus.xml](scrob-omnibus/scrob-omnibus.xml) | `bellamy/scrob:latest-omnibus` | All-in-one container with embedded PostgreSQL |

## Install (Community Applications)

1. In Unraid, open **Apps** (Community Applications) and search for **Scrob** / **scrob-omnibus**.
2. Install the template, set **SECRET_KEY** (`openssl rand -hex 32`) and timezone, then **Apply**.
3. Open the WebUI on port **7330**, then follow the official [first-run guide](https://github.com/ellite/scrob#first-setup) (create account, TMDB API key, connect media servers, first sync).

Official docs: [scrob.app](https://scrob.app) · [ellite/scrob README](https://github.com/ellite/scrob#getting-started) (includes [omnibus](https://github.com/ellite/scrob#omnibus-single-container) details)

Template support: [Unraid forum topic](https://forums.unraid.net/topic/199294-support-jorgen-scrob-omnibus/).

Scrob app issues: [ellite/scrob](https://github.com/ellite/scrob/issues).

## Alternative install (manual template)

1. Copy `scrob-omnibus/scrob-omnibus.xml` to your flash drive:  
   `/boot/config/plugins/dockerMan/templates-user/my-scrob-omnibus.xml`
2. In Unraid: **Docker → Add Container → Template** → select **scrob-omnibus**
3. Set **SECRET_KEY** (`openssl rand -hex 32`), timezone, then **Apply**
4. Open WebUI on port **7330**, then follow the official [first-run guide](https://github.com/ellite/scrob#first-setup)

## OIDC / SSO (optional)

Scrob supports any standards-compliant OpenID Connect provider (Authelia, Authentik, Keycloak, Google, etc.). The omnibus template exposes the common variables; leave **Enable OIDC / SSO** as `false` unless you need them.

1. Put Scrob behind a reverse proxy with HTTPS (NPM, SWAG, Traefik, …).
2. Register a confidential OIDC client at your IdP with redirect URI  
   `https://your-scrob-host/oidc-callback`.
3. In the Unraid template, set at least:
   - **Enable OIDC / SSO** → `true`
   - **OIDC Client ID** / **OIDC Client Secret**
   - **OIDC Auth / Token / UserInfo URLs** (from your IdP)
   - **OIDC Redirect URL** → `https://your-scrob-host/oidc-callback`
   - **OIDC Discovery URL** → `https://your-idp/…/.well-known/openid-configuration`  
     (**recommended** — turns on `id_token` verification and stable `(issuer, sub)` binding)
4. Optionally set **Server URL** to the same public `https://your-scrob-host`.
5. Apply / recreate the container, then use **Login with …** on the Scrob login page.

PKCE is on by default in current Scrob releases. Advanced escape hatches (`OIDC_PKCE`, `OIDC_ISSUER` / `OIDC_JWKS_URL`, logout URLs) are not in the template — add them as extra variables if needed, or see upstream docs.

Full behaviour (linking, unlink, MFA, logout): [OIDC / Single Sign-On](https://github.com/ellite/scrob#oidc--single-sign-on) in the Scrob README.

## License

MIT — template metadata and XML only. [Scrob](https://github.com/ellite/scrob) is licensed under GPL-3.0.
