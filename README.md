# Minecraft Server Infrastructure

This repository contains the docker infrastructure stuff for the minecraft server I host.
I've put this here in case anyone may find it helpful.
It provides both a configuration for rootfull docker and rootless podman (No guarantees for the rootless version :)).

## Deploy it yourself

Run one of the provided ansible playbooks for either a rootful (reccomended) or rootless install.
Following that, a few more customization steps need to be run.

### Rootful

1. Navigate to `/srv/minecraft-infra`
2. Move `.env.example` to `.env` and customize passwords and key
3. Replace the certificate and key in `caddy/` or just use [ACME](https://caddyserver.com/docs/automatic-https)
4. Start the service using `systemctl start minecraft-infra.service`
5. Create an admin user using `docker exec -it minecraft-infra-panel-1 /pufferpanel/bin/pufferpanel user add` (May take a while)

### Rootless

1. Navigate to `/srv/minecraft/infra`
2. Move `.env.example` to `.env` and customize passwords and key
3. Replace the certificate and key in `caddy/` or use [ACME](https://caddyserver.com/docs/automatic-https)
4. Start the service using `systemctl -M minecraft@ --user start minecraft-infra.service`
5. Export the podman socket for use with docker using `export DOCKER_HOST=unix:///run/user/$(id -u minecraft)/podman/podman.sock`
6. Create an admin user using `docker exec -it minecraft-infra-panel-1 /pufferpanel/bin/pufferpanel user add` (May take a while)
