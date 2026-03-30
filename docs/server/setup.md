# Server Setup — Proxmox VE

Proxmox is the main server running all VMs and LXC containers. It's also where the NAS storage is mounted and shared into services.

## Hardware

:::
## Installation

- **Version:** Proxmox VE 8.x
- Installed from USB, booted directly into the web UI at `https://<ip>:8006`
- After install, ran the [Proxmox community post-install script](https://tteck.github.io/Proxmox/) to remove the enterprise repo subscription nag and enable the no-subscription repo

## Network Setup

Proxmox uses Linux bridges to connect VMs and containers to the OPNsense VLANs. The physical NIC is connected to the router as a VLAN trunk, and each bridge maps to a VLAN.

| Bridge | VLAN | Network |
| ------ | ---- | ------- |
| vmbr10 | 10   | LAN     |
|        |      |         |
|        |      |         |

:::

## Storage

| Pool      | Type      | Used for                      | Size |
| --------- | --------- | ----------------------------- | ---- |
| local     | LVM       | Boot, ISO images              |      |
| local-zfs | ZFS       | VM and CT disks               |      |
| nas       | NFS mount | Shared media and data storage |      |

## VMs vs Containers

Containers (LXC) are used for lightweight services where a full OS isn't needed, and VMs are used when the service needs its own kernel or better isolation, like the NAS or anything that needs direct hardware access, although I prefer to use VMs with docker installed to run containers.

[[vms]] for the full list of what's running.

## Backups

Proxmox has built-in backup via `vzdump`. 

Backups are scheduled weekly and stored on the NAS mount.

- `Datacenter → Backup → Add`
- Retention: keep last 5 backups per VM/CT
- Backup storage: nas pool

## Notes

- Web UI runs on port 8006 — currently accessible from LAN (MGMT VLAN planned, see vlans.md)
- Root login over SSH is disabled, key-based auth only
- Proxmox user `admin` created for daily use instead of root