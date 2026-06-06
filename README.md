# Unraid templates for Scrob

Community-maintained [Unraid](https://unraid.net/) Docker templates for [Scrob](https://github.com/ellite/scrob) — self-hosted media tracking for Jellyfin, Plex, and Emby.

**This repository is not affiliated with the Scrob author.** It packages the official `bellamy/scrob` Docker images for Unraid users. Template install and Unraid-specific setup questions belong here; application bugs and feature requests go to [ellite/scrob](https://github.com/ellite/scrob/issues).

## Templates

| Template                                             | Image                          | Description                                   |
| ---------------------------------------------------- | ------------------------------ | --------------------------------------------- |
| [scrob-omnibus.xml](scrob-omnibus/scrob-omnibus.xml) | `bellamy/scrob:latest-omnibus` | All-in-one container with embedded PostgreSQL |

## Quick install (manual)

1. Copy `scrob-omnibus/scrob-omnibus.xml` to your flash drive:  
   `/boot/config/plugins/dockerMan/templates-user/my-scrob-omnibus.xml`
2. In Unraid: **Docker → Add Container → Template** → select **scrob-omnibus**
3. Set **SECRET_KEY** (`openssl rand -hex 32`), timezone, then **Apply**
4. Open WebUI on port **7330**, then follow the official [first-run guide](https://github.com/ellite/scrob#first-setup) (create account, TMDB API key, connect media servers, first sync)

Official docs: [scrob.app](https://scrob.app) · [ellite/scrob README](https://github.com/ellite/scrob#getting-started) (includes [omnibus](https://github.com/ellite/scrob#omnibus-single-container) details)

Template support: [Unraid forum topic](https://forums.unraid.net/topic/199294-support-jorgen-scrob-omnibus/).

Scrob app issues: [ellite/scrob](https://github.com/ellite/scrob/issues).

## License

MIT — template metadata and XML only. [Scrob](https://github.com/ellite/scrob) is licensed under GPL-3.0.
