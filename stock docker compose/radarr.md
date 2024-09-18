``` yaml
services:
  radarr:
    icon: https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/Radarr/icon.png
    network_mode: container:gluetun
    image: ghcr.io/hotio/radarr
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=US/Central
    restart: unless-stopped 
    volumes:
      - /DATA/AppData/radarr/config:/config
      - /mnt/media/movies:/data
```
[source](https://hotio.dev/containers/radarr/)