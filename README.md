# traefik-swarm

## What?

Sets up a dynamic Traefik reverse proxy on Docker Swarm


## How?

### Role Usage

Traefik is designed to dynamically configure, so there isn't much to do ahead of time. See [`defaults/main.yml`](defaults/main.yml).

### Traefik Usage

Traefik is a dynamic reverse proxy. It will watch the Docker socket for new containers it needs to proxy. The key is adding some deploy labels to the container. The core properties are shown below but there are [*many* others](https://docs.traefik.io/configuration/commons/).


  app1:
    image: myuser/app1
    ...
    deploy:
      placement:
        constraints:
          - node.role == worker
      labels:
        traefik.port: 5000
        traefik.backend: app1
        traefik.domain: app1.domain.com
        traefik.backend.healthcheck.path: /health
