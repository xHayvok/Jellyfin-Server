``` yaml
services:
  sonarr:
    icon: https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/Sonarr/icon.png
    network_mode: container:gluetun
    image: ghcr.io/hotio/sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=US/Central
    restart: unless-stopped 
    volumes:
      - /DATA/AppData/sonarr/config:/config
      - /mnt/media/shows:/data
```
[source](https://hotio.dev/containers/sonarr/)