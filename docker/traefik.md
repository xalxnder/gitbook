---
icon: traffic-light
---

# Traefik



{% code fullWidth="true" %}
```yaml
services:

  traefik:
    image: "traefik:v3.5"  # Use Traefik version 3.5
    container_name: "traefik"  # Name the container "traefik"

    command:
      #- "--log.level=DEBUG"  # Uncomment for detailed Traefik logs (useful for troubleshooting)
      - "--api.insecure=true"  # Enable the Traefik web UI (dashboard) on port 8080 (insecure, for local use only)
      - "--providers.docker=true"  # Enable Docker provider to discover containers with labels
      - "--providers.docker.exposedbydefault=false"  # Only expose containers with traefik.enable=true
      - "--entryPoints.websecure.address=:443"  # Define an entry point named "websecure" listening on port 443
      - "--certificatesresolvers.myresolver.acme.tlschallenge=true"  # Use TLS challenge for Let's Encrypt certificate resolution
      #- "--certificatesresolvers.myresolver.acme.caserver=https://acme-staging-v02.api.letsencrypt.org/directory"
        # Use Let's Encrypt staging server for testing (prevents rate limiting, uncomment if testing)
      - "--certificatesresolvers.myresolver.acme.email=postmaster@example.com"  # Email used for Let's Encrypt registration
      - "--certificatesresolvers.myresolver.acme.storage=/letsencrypt/acme.json"  # Where Traefik stores certificates

    ports:
      - "443:443"  # Expose HTTPS (websecure entrypoint) to the host
      - "8080:8080"  # Expose Traefik dashboard (if api.insecure=true)

    volumes:
      - "./letsencrypt:/letsencrypt"  # Persist Let's Encrypt certs on host
      - "/var/run/docker.sock:/var/run/docker.sock:ro"  # Give Traefik read-only access to Docker socket

  whoami:
    image: "traefik/whoami"  # A simple web service that returns request info
    container_name: "simple-service"  # Name this container

    labels:
      - "traefik.enable=true"  # Enable this service to be picked up by Traefik
      - "traefik.http.routers.whoami.rule=Host(`whoami.example.com`)"  # Route traffic with this hostname
      - "traefik.http.routers.whoami.entrypoints=websecure"  # Use the "websecure" entry point (HTTPS)
      - "traefik.http.routers.whoami.tls.certresolver=myresolver"  # Use the defined certificate resolver to get certs
```
{% endcode %}
