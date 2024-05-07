# Docker Compose deployment for Saltcorn with Traefik and Let's Encrypt

> The source of this repository is extracted from [Saltcorn](https://github.com/saltcorn/saltcorn).

## Introduction
This repository contains a `docker-compose` configuration for deploying [Saltcorn](https://github.com/saltcorn/saltcorn) as a containerized application with [Traefik](https://traefik.io/) as a reverse proxy and [Let's Encrypt](https://letsencrypt.org/) for TLS certificates. It is based on the official [Saltcorn Docker image](https://hub.docker.com/r/saltcorn/saltcorn) and the [PostgreSQL Docker image](https://hub.docker.com/_/postgres).

## Usage

- Clone this repository `git clone` or download `docker-compose.yml`, `docker-entrypoint-initbd.sql` in a directory of your choice.

- Create a .env file with the following content:

```
PGDATABASE=saltcorn
PGUSER=postgres
PGPASSWORD=dbpassword
DOMAIN=yourdomain
SALTCORN_SECRET=hashsecret
SALTCORN_SESSION_SECRET=sessionsecret
SALTCORN_MULTI_TENANT=true
SALTCORN_FILE_STORE=/saltcorn_files
```

Delete the `SALTCORN_MULTI_TENANT` line if you dont want to use the multi-tenan feature.
Delete the `SALTCORN_FILE_STORE` line if you dont want to use the default user XRD.

- Deploy the docker-compose file using `docker-compose up -d`

Traefik has to be configured with two entrypoints, web and websecure, and it can be accesses through the web entrypoint on port 80 with saltcorn.docker.localhost or through the websecure entrypoint on port 443 with subdomain.domain. A properly configured Traefik instance is required for this to work, test configuration are provided in the `traefik` directory, or the traefik configuration in docker-compose.yml can be updated to fit your needs.

Also your domain DNS server has to be configured to point to the Traefik instance with the configured domain. 

## License
All code in this repository is licensed under the terms of the `MIT License`. For further information please refer to the `LICENSE` file.