# Services

Overview of all self-hosted services running on the Proxmox server.

## Running

| Service  | Purpose         | VM/CT  | Port | Docs          |
| -------- | --------------- | ------ | ---- | ------------- |
| Jellyfin | Media streaming | CT 101 | 8096 | [jellyfin.md] |
|          |                 |        |      |               |

## Planned

| Service | Purpose                    | Status      |
| ------- | -------------------------- | ----------- |
| Grafana | Dashboards / observability | Planned     |

## Notes

- All services are inside my private network but the DMZ part
- VLAN X is dedicated to services — see [[vlans]]