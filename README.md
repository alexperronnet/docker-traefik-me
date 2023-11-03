# Automated traefik DNS resolver with SSL

A fork of [Pyrou Gist](https://gist.github.com/pyrou/4f555cd55677331c742742ee6007a73a) with some modifications that allow you to have local services accessible by myservice.traefik.me with [let's encrypt](https://letsencrypt.org/) SSL certificates without any system configuration.

## What is this?

This project allow you to run inside your dev machine a dynamic traefik gateway that will add any services and provide a ssl certificate for any domain under traefik.me.

You can add your services under the external network 'traefik'.

## Getting started

1. Start the traefik gateway

   ```bash
   docker-compose up -d
   ```

   > Traefik dashboard is now available at [dashboard.traefik.me](https://dashboard.traefik.me)

2. Add your services

   ```bash
    services:
    web:
        networks:
            - traefik
        labels:
            - "traefik.http.routers.example.rule=Host(`example.traefik.me`)"
            - "traefik.http.routers.example-tls.tls.domains[0].main=example.traefik.me"
            - "traefik.http.routers.example-tls.tls.domains[0].sans=example-*.traefik.me"
            - "traefik.http.routers.example.tls=true"

    networks:
    traefik:
        external: true
   ```

   > Your service is now available at [example.traefik.me](https://example.traefik.me)

## Credits

Thanks to [Pyrou](https://github.com/pyrou).

- [Traefik.me](http://traefik.me/)
- [Source](https://github.com/pyrou/traefik.me)
- [Base configuration](https://gist.github.com/pyrou/4f555cd55677331c742742ee6007a73a)
