``` yaml
services:
  prowlarr:
    icon: https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/Prowlarr/icon.png
    network_mode: container:gluetun
    image: ghcr.io/hotio/prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - UMASK=002
      - TZ=US/Central
    restart: unless-stopped 
    volumes:
      - /DATA/AppData/prowlarr/config:/config
```
[source](https://hotio.dev/containers/prowlarr/)