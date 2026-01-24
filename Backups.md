## **Step 1 — Backup Proxmox Host Configuration**

> Why first: Without host configs, you can’t restore VM definitions if Proxmox breaks.

1. Backup critical configs:
2. `/etc/pve/          ← VM definitions, storage, snapshots /etc/network/      ← networking /root/.ssh/        ← SSH keys /etc/cron.*        ← backup scripts, schedules`
    
3. Optional: Export cluster DB (for single node, just `/etc/pve` is enough)
    
4. Store in backup dataset (`/backups`) as `proxmox-config-YYYYMMDD.tar.gz`
    
5. Automate weekly if desired
    

---

## **Step 2 — Backup VMs**

> Why second: The VM is the unit that holds all data (TrueNAS, Docker, OPNsense, others).

1. Use **Proxmox snapshot backups** for all VMs:
    
    - TrueNAS VM
        
    - Docker VM
        
    - OPNsense VM
        
    - Other 7 VMs
        
2. Backup mode: **Snapshot** (no downtime)
    
3. Compression: **ZSTD**
    
4. Retention: 3–5 daily, optional 1 weekly
    
5. Store backups in your `/backups` dataset
    

---

## **Step 3 — Snapshot VMs (temporary undo before updates)**

> Why: Gives you a quick rollback point before you apply updates.

- Take snapshots **per VM** you plan to update:
    

- `vmname-preupdate-YYYYMMDD`
    
- Only keep for 1–3 days, delete afterward
    

---

## **Step 4 — Backup internal VM configs (optional but recommended)**

- **Docker VM**: backup important configs inside the VM
    
    - `docker-compose.yml`
        
    - Database dumps
        
    - Volume data if needed
        
- **OPNsense VM**: export config from the GUI:
    
    - System → Backup / Restore → Download configuration
        
- **TrueNAS VM**: optional if you want dataset-level snapshots inside TrueNAS (extra protection)
    

> These are **small files** — can be stored in `/backups` or off-box if available

---

## **Step 5 — Update VMs**

> After host configs and VM backups are safe.

- Security updates / OS updates on all VMs
    
- Docker VM: use Watchtower with **opt-in** containers
    
- TrueNAS VM: apply updates carefully
    
- OPNsense VM: apply updates from GUI (backup config first!)
    

---

## **Step 6 — Verify everything**

- Boot VMs if needed
    
- Test critical services: Docker containers, TrueNAS shares, OPNsense routing/firewall
    

---

## **Step 7 — Delete temporary snapshots**

- Only keep the permanent Proxmox backups
    
- Remove `vmname-preupdate-*` snapshots after confirming everything is working
    

---

## **Step 8 — Weekly “lab hygiene”**

- Check backups succeeded
    
- Delete old backups to free space
    
- Export critical configs (Proxmox, Docker VM, TrueNAS, OPNsense) off-box if possible
    
- Monitor disk usage in `/backups` and `vmdata`