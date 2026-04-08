# Services

Overview of all self-hosted services running on the Proxmox server.

## Running

- **nextcloud** — Self-hosted cloud (files, sync, sharing)
- **nextcloud_db (MariaDB)** — Database backend for Nextcloud
- **navidrome** — Music streaming server (Subsonic-compatible)
- **lidarr** — Music library management and automation
- **prowlarr** — Indexer manager (feeds Lidarr/qBittorrent)
- **qbittorrent** — Torrent client (downloads automation target)
- **flaresolverr** — Anti-bot/CAPTCHA bypass for indexers
- **jellyfin** — Media server (movies/series streaming)

---

## Planned

| Service | Purpose                    | Status  |
| ------- | -------------------------- | ------- |
| Grafana | Dashboards / observability | Planned |

## Notes

- All services are inside my private network but the DMZ part
- VLAN X is dedicated to services — see [[vlans]]