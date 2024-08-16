# Brionne

Caddy-based reverse proxy for authenticating B4CKSP4CE residents with Teleport App Access.

## Example

Docker Compose:

```yaml
services:
  authproxy:
    image: ghcr.io/b4ck5p4c3/brionne:latest
    restart: unless-stopped
    security_opt:
      - no-new-privileges:true
    cap_add:
      - NET_ADMIN
    ports:
      - "127.0.0.1:1337:80"
    environment:
      - UPSTREAM="http://whoami"
    networks:
      - internal

  whoami:
    image: traefik/whoami
    restart: unless-stopped
    hostname: whoami
    expose:
      - 80
    networks:
      - internal

networks:
  internal:
```
