``` yaml
services:
  lidarr:
    icon: https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/Lidarr/icon.png
    network_mode: container:gluetun
    image: ghcr.io/hotio/lidarr
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=US/Central
    restart: unless-stopped 
    volumes:
      - /DATA/AppData/lidarr/config:/config
      - /mnt/media/music:/data
``` 
[source](https://hotio.dev/containers/lidarr/)