``` yaml
services:
  bazarr:
    icon: https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/Bazarr/icon.png
    network_mode: container:gluetun
    image: ghcr.io/hotio/bazarr
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=US/Central
    restart: unless-stopped 
    volumes:
      - /DATA/AppData/bazarr/config:/config
      - /mnt/media/subtitles:/data
```
[source](https://hotio.dev/containers/bazarr/)