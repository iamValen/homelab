# Router Setup — OPNsense

OPNsense is running as the main router and firewall for the homelab. It handles all inter-VLAN routing, firewall rules, DNS, VPN, and ad blocking.

## Hardware

::::
## Installation

- **Version:** OPNsense
- After install, SSH and web UI access confirmed from LAN before proceeding

## Interface Setup

| Interface | Role      | Notes                          |
| --------- | --------- | ------------------------------ |
| igb0      | WAN       | DHCP from ISP                  |
| re0       | LAN trunk | Tagged VLANs to Proxmox server |

VLANs are trunked through a single interface to the server. See vlans.md for the full breakdown.

## Plugins Installed

| Plugin       | Purpose                           |
| ------------ | --------------------------------- |
| os-wireguard | VPN for remote access             |
|              |                                   |

## DNS

Using OPNsense as the local DNS resolver (Unbound). All VLANs use the router as their DNS server, which also lets the ad blocker work network-wide.

## DHCP

Each VLAN has its own DHCP pool. The server and NAS have static leases so their IPs never change.

::::::::

## Backups

OPNsense config can be exported as an XML file from the web UI.

- `System -> Configuration -> Backups`
- Stored in local pc
- Should be done before and after any major change

## Notes

- Web UI runs on port 443 (HTTPS) on the LAN interface
- SSH is enabled for local access only
- Default admin user has been renamed and created a personal user