---
icon: traffic-light
---

# Traefik

Traefik service example. Full list of cli flags can be found [here](https://doc.traefik.io/traefik/reference/static-configuration/cli/).

{% code fullWidth="true" %}
```yaml
services:

  traefik:
    image: "traefik:v3.5"
    
    # Name the container "traefik"
    container_name: "traefik"

    command:
      # Uncomment for detailed Traefik logs (useful for troubleshooting)
      #- "--log.level=DEBUG"

      # Enable the Traefik web UI (dashboard) on port 8080 (insecure, for local use only)
      - "--api.insecure=true"

      # Enable Docker provider to discover containers with labels
      - "--providers.docker=true"

      # Only expose containers with traefik.enable=true
      - "--providers.docker.exposedbydefault=false"

      # Define an entry point named "websecure" listening on port 443
      - "--entryPoints.websecure.address=:443"

      # Use TLS challenge for Let's Encrypt certificate resolution
      - "--certificatesresolvers.myresolver.acme.tlschallenge=true"

      # Use Let's Encrypt staging server for testing (prevents rate limiting, uncomment if testing)
      #- "--certificatesresolvers.myresolver.acme.caserver=https://acme-staging-v02.api.letsencrypt.org/directory"

      # Email used for Let's Encrypt registration
      - "--certificatesresolvers.myresolver.acme.email=postmaster@example.com"

      # Sets a number of seconds to wait before checking the DNS challenge TXT record for actual propagation
      - "--certificatesresolvers.cloudflare.acme.dnschallenge.propagation.delaybeforechecks=30"

      # Where Traefik stores certificates
      - "--certificatesresolvers.myresolver.acme.storage=/letsencrypt/acme.json"

    ports:
      # Expose HTTPS (websecure entrypoint) to the host
      - "443:443"

      # Expose Traefik dashboard (if api.insecure=true)
      - "8080:8080"

    volumes:
      # Mount host directory to persist Let's Encrypt certs (stored in acme.json)
      - "./letsencrypt:/letsencrypt"

      # Give Traefik read-only access to Docker socket
      - "/var/run/docker.sock:/var/run/docker.sock:ro"

  whoami:
    image: "traefik/whoami"

    # Name this container
    container_name: "simple-service"

    labels:
      # Enable this service to be picked up by Traefik
      - "traefik.enable=true"

      # Route traffic with this hostname
      - "traefik.http.routers.whoami.rule=Host(`whoami.example.com`)"

      # Use the "websecure" entry point (HTTPS)
      - "traefik.http.routers.whoami.entrypoints=websecure"

      # Use the defined certificate resolver to get certs
      - "traefik.http.routers.whoami.tls.certresolver=myresolver"
```
{% endcode %}



### Testing Certs

> If you un-commented the `acme.caserver` line, you will get an SSL error, but if you display the certificate and see it was emitted by `Fake LE Intermediate X1` then it means all is good. (It is the staging environment intermediate certificate used by Let's Encrypt). You can now safely comment the `acme.caserver` line, remove the `letsencrypt/acme.json` file and restart Traefik to issue a valid certificate.
