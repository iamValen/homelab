Disabled SSH via password and only with key.

**SSH keys** = stronger, safer, and more flexible
**Password login** = weak, can be guessed, stolen or cracked

### Create an SSH key (on your local machine)

From local machine:
`ssh-keygen -t ed25519`


### Copy your public key to the Debian server

From local machine:
`ssh-copy-id user@server_ip`

Or manually:

`cat ~/.ssh/id_ed25519.pub | ssh user@server_ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"`


### Disable password authentication in SSH

On the server:

`sudo nano /etc/ssh/sshd_config`

Set (or update) these lines:

```
PasswordAuthentication no 
ChallengeResponseAuthentication no 
UsePAM no
```

(Optional but recommended)

`PermitRootLogin no`

Save and exit.


### Restart SSH

`sudo systemctl restart ssh`