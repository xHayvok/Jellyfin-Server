``` yaml
services:
  readarr:
    icon: https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/Readarr/icon.png
    network_mode: container:gluetun
    image: ghcr.io/hotio/readarr
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=US/Central
    restart: unless-stopped 
    volumes:
      - /DATA/AppData/readarr/config:/config
      - /mnt/media/books:/data
```
[source](https://hotio.dev/containers/readarr/)