
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
		