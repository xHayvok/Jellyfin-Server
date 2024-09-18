``` yaml
services:
  qbittorrent:
    icon: https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/qBittorrent/icon.png
    network_mode: container:gluetun
    image: ghcr.io/hotio/qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=US/Central
    restart: unless-stopped 
    volumes:
      - /DATA/AppData/qbittorrent/config:/config
      - /mnt/downloads:/data
```
[source](https://hotio.dev/containers/qbittorrent/)