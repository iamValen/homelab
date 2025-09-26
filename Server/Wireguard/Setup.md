
- Create a directory dedicated to the Wireguard docker-compose
- Create `docker-compose.yml`
(version with DuckDNS Setup)

```bash
version: '3.8'
services:
  wireguard:
    image: linuxserver/wireguard:latest
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Lisbon
      - SERVERURL=<full-domain>    # Change
      - SERVERPORT=51820
      - PEERS=5
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.13.13.0
      - ALLOWEDIPS=0.0.0.0/0
      - LOG_CONFS=true
    volumes:
      - ./config:/config
      - /lib/modules:/lib/modules:ro
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped

  duckdns:
    image: lscr.io/linuxserver/duckdns:latest
    container_name: duckdns
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Lisbon
      - SUBDOMAINS=<subdomain>    # Change
      - TOKEN=<TOKEN>             # Change 
      - UPDATE_IP=ipv4
      - LOG_FILE=true
    volumes:
      - ./duckdns-config:/config
    restart: unless-stopped
    ```

To start the containers run (in the same dir as `docker-compose.yml`):
```docker compose up -d```

To stop:
`docker compose down`

To check status:
`docker ps`