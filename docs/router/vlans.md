# VLANs

The network is segmented into 6 VLANs to keep different types of traffic isolated from each other. The main goal is to make sure that if something gets compromised (say, an IoT device, a guest or the ), it can't reach anything sensitive.

## Segments

|VLAN|Name|Purpose|
|---|---|---|
|10|LAN|Trusted daily-use devices|
|20|SERVER|Proxmox VMs and self-hosted services|
|30|DMZ|Internet-facing services (reverse proxy, etc.)|
|40|IOT|IoT devices, fully isolated|
|50|GUEST|Guest devices, internet only|
|99|MGMT|Proxmox and OPNsense admin interfaces|

---

## Firewall Rules

### LAN (10)

The main trusted network. Can reach services on the SERVER VLAN through specific ports only - not open access. Can't reach DMZ directly since anything there is meant to be accessed from outside via WireGuard.

- ✅ Internet access
- ✅ SERVER — specific ports only (e.g. 8096 for Jellyfin)
- ❌ DMZ
- ❌ IOT
- ❌ GUEST
- ❌ MGMT

### SERVER (20)

Hosts all the VMs and self-hosted services. It can talk back to the NAS and reach the internet for updates, but it should never initiate connections into the LAN. Services are consumed by LAN, not the other way around.

- ✅ Internet access
- ✅ DMZ — specific back-end ports only
- ❌ LAN (server doesn't call home)
- ❌ IOT
- ❌ GUEST
- ❌ MGMT

### DMZ (30)

Anything that's exposed to the internet lives here, like a reverse proxy. It can talk to the SERVER on specific ports it needs, but has no business touching anything else internally.

- ✅ Internet access
- ✅ SERVER — specific ports only
- ❌ LAN
- ❌ IOT
- ❌ GUEST
- ❌ MGMT

### IOT (40)

IoT devices get internet and nothing else. These devices tend to have poor security so the less they can reach, the better.

- ✅ Internet access
- ❌ Everything internal

### GUEST (50)

Same idea as IOT. Guests get internet, that's it.

- ✅ Internet access
- ❌ Everything internal

### MGMT (99)

Where Proxmox and OPNsense admin interfaces will live. No internet, no access from general VLANs — only reachable from a specific trusted machine on LAN. **Not implemented yet.**

- ❌ Internet
- ❌ All VLANs (inbound and outbound)
- ✅ Designated trusted machine on LAN only

---

## Status

|VLAN|Status|
|---|---|
|10 — LAN|✅ Done|
|20 — SERVER|✅ Done|
|30 — DMZ|✅ Done|
|40 — IOT|✅ Done|
|50 — GUEST|✅ Done|
|99 — MGMT|🔲 Planned — admin UIs still accessible from LAN for now|

## Roadmap

- [ ] Create MGMT VLAN 99 on OPNsense
- [ ] Move Proxmox web UI (port 8006) to MGMT segment
- [ ] Move OPNsense admin interface to MGMT segment
- [ ] Restrict MGMT access to a single trusted machine