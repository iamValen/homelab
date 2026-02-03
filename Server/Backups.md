
# OPNsense

Just a downloadable file.


# Proxmox

To backup the entire proxmox here's two different things to look out:
- Backup VMs/CTs
- Backup Proxmox Config


### VMs / CTs

This is done by creating a scheduled backup in the Proxmox **Datacenter > Backups**.


### Proxmox Config

It's the config files inside the proxmox host, here I created a bash script that saves the wanted files to a mounted NFS share in /etc/fstab:

```bash
#!/bin/bash

DATA=$(date +%Y-%m-%d)
DEST="/mnt/backups/proxmox-config"

mkdir -p $DEST

tar -czf $DEST/proxmox-config-$DATA.tar.gz \
    /etc/pve \
    /etc/network \
    /etc/hosts \
    /etc/resolv.conf \
    /etc/fstab \
    /root

find "$DEST" -type f -name "*.tar.gz" -mtime +14 -delete 
#delete backups from +14 days
```

Then I created a CRON job:
```bash
crontab -e
```

Every day at 2:30 AM
```bash
30 2 * * * /root/backup-proxmox-config.sh
```