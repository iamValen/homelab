
- [ ] Automatic Updates
- [ ] 2 x 3D prints
- [ ] SSH Access Management
- [ ] VLANs
- [ ] OPNsense Firewall
- [ ] VMs/CTs Firewall
- [ ] [[Reverse Proxy]] - https://www.apalrd.net/posts/2023/network_acme/
- [ ] IDS/IPS na Web VLAN
- [x] NextCloud

---


- [x] Wireguard VPN
- [x]  Dynamic DNS
- [x] Films/Series Media Server – servidor de mídia extra
- [x] Music Media Server – entretenimento e prática de containers
- [ ] Obsidian Sync
- [ ] Python Flask App in Docker – aprendizado de containers e apps
- [ ] Camera monitorization – monitoramento de câmeras
- [ ] Camera Setup - Person Recognition – reconhecimento de pessoas
- [ ] Self-host Website


---
---
---

# In depth

- [ ] Backups of current config
	- Router config
	- Switch config (especially if VLANs will be added)
	- DNS config (if separate service)
	- Firewall rules

- [ ] Verify you can **restore**, not just that a backup file exists.

---

- [ ] Router backup (system-level)
- [ ] FIX WireGuard not being able to SSH into local LANs
- [ ] FIX Nextcloud previews
	- [ ] Mount NAS to Docker and Generate Preview for each file inside cloud (.HEIC, .MOV extensions)
	- [ ] Cron job for it to generate it each week
- [ ] Create OPNsense User

---

- [ ] Plan VLANs setup and look what has to change and future configs
	
	Before applying:
	- VLAN IDs
	- Subnets per VLAN
	- Gateway IPs
	- Which ports are tagged/untagged
	- Which VLANs can talk to which others

---

- [ ] Integrate VLANs (network structure)
	
	Implementation order:
	1. Create VLANs on router
	2. Create VLANs on switches
	3. Assign ports carefully
	4. Test basic connectivity per VLAN

---

- [ ] Router tweaks
	- [ ] Ad block
	- [ ] IDS/IPS
	- [ ] Firewall rules

- [ ] Backup Router again
