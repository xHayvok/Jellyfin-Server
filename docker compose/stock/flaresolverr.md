``` yaml
services:
  flaresolverr:
    icon: https://avatars.githubusercontent.com/u/10577978
    network_mode: container:gluetun
    # DockerHub mirror flaresolverr/flaresolverr:latest
    image: ghcr.io/flaresolverr/flaresolverr:latest
    environment:
      - LOG_LEVEL=info
      - LOG_HTML=false
      - CAPTCHA_SOLVER=none
      - TZ=US/Central
	  - PROMETHEUS_ENABLED=false
	  - PROMETHEUS_PORT=8191
	  - PORT=8191
    restart: unless-stopped 
```
[source](https://hub.docker.com/r/flaresolverr/flaresolverr)