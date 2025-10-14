1. Share storage with the NAS - [[Share Storage]]
2. Install curl and then install docker with:
```
	curl -fsSL https://get.docker.com -o get-docker.sh
	sudo sh get-docker.sh
	sudo docker run hello-world 
```
3. Install Navidrome (or other services)
```
services:
  navidrome:
    image: deluan/navidrome:latest
    user: 1000:1000 # should be owner of volumes
    ports:
      - "4533:4533"
    restart: unless-stopped
    environment:
      # Optional: put your config options customization here. Examples:
      # ND_LOGLEVEL: debug
    volumes:
      - "/path/to/data:/data"
      - "/path/to/your/music/folder:/music:ro"
```
4. Run docker compose: `docker compose up -d`
5. `docker ps` to check containers