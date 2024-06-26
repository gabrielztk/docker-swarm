# Steps taken to deploy Traefik stack

Based on guide by [Docker Swarm Rocks](https://dockerswarm.rocks/traefik/)

## Prepare environment variables

Create a network for trafik

    docker network create --driver=overlay traefik-public

Get manager node ID

    export NODE_ID=$(docker info -f '{{.Swarm.NodeID}}')

Create certificate tag on manager

    docker node update --label-add traefik-public.traefik-public-certificates=true $NODE_ID

Export email for letsencrypt

    export EMAIL=example@here.net

Export the duckdns token for letsencrypt

    export DUCKDNS_TOKEN=token.here

Export base domain

    export BASE_DOMAIN=your.domain.here

Export you username for the traefik UI

    export USERNAME=admin

Export you password interactively

    export HASHED_PASSWORD=$(openssl passwd -apr1)

## Deploy Traefik

    docker stack deploy -d -c docker-compose.yml traefik
