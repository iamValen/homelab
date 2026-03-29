
1. `sudo apt install cifs-utils`
2. `mkdir /mnt/<dataset>`
3. Edit `sudo nano /etc/fstab`
	In the end of /etc/fstab add a line like this:
		`//<nas ip>/<dataset> /mnt/<dataset> cifs credentials=/root/smbcredentials,uid=<NAS usr id>,gid=<NAS grp id> 0 0`
		Example
		//192.168.1.106/media /mnt/media cifs credentials=/root/smbcredentials,uid=3000,gid=3000 0 0
4. Create `/root/smbcredentials`
	`sudo nano /root/smbcredentials`
	And insert:
		`user:<NAS user>
		`password:<NAS user password>`

## Script to make sure fstab mount work on Server Boot
In some cases the system doesn't start or wait for the NAS to boot up and will not mount the shared storage correctly so this ensures that it's mounted automatically.

1. `sudo nano /usr/local/bin/mount_nas_on_boot.sh`
2. 
   ```bash
#!/bin/bash
 Wait for NAS to respond, then mount all filesystems

NAS_IP="192.168.1.106"

echo "Waiting for ($NAS_IP) to respond..."
until ping -c1 "$NAS_IP" &>/dev/null; do
    sleep 5
done

echo "NAS is reachable. Waiting 30 seconds before mounting..."
sleep 30

systemctl daemon-reload
mount -a

cd /opt/docker/
docker compose down
docker compose up -d

echo "Mount complete."```
3. `sudo chmod +x /usr/local/bin/mount_nas_on_boot.sh`
4. `sudo nano /etc/systemd/system/mount-nas.service`
5. 
```bash
[Unit]
Description=Wait for NAS and mount filesystems
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/mount_nas_on_boot.sh
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```
6. `sudo systemctl daemon-reload`
7. `sudo systemctl enable mount-nas.service 
8. `sudo systemctl start mount-nas.service`

Check logs with: `sudo journalctl -u mount-nas.service -f`

