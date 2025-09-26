# Desktop
### Quick Start up
`sudo wg-quick up wg0`

If it's already running stop it with

`sudo wg-quick down <name of the .conf file> (without .conf)`

### Setup
Copy your peer config file (e.g. peer1.conf) to `/etc/wireguard`
### Check Status
`sudo wg`

---

# Phone
In the Docker Machine with WireGuard setup run:
```docker-compose logs wireguard```

Use the QR Code to connect to an unused PEER using WireGuard Mobile App.

Activate it.