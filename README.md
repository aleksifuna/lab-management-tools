# Lab Management Tools

A lightweight Docker Compose setup for running local lab management utilities:

- Portainer CE for Docker management
- pgAdmin 4 for PostgreSQL administration

## Stack

- Portainer: `portainer/portainer-ce:latest`
- pgAdmin: `dpage/pgadmin4`

## Prerequisites

- Docker installed
- Docker Compose available (`docker compose`)

## Project Structure

- `docker-compose.yaml`

## Quick Start

Start the stack in detached mode:

```bash
docker compose up -d
```

Check running containers:

```bash
docker compose ps
```

Stop the stack:

```bash
docker compose down
```

Stop and remove volumes (this deletes Portainer data):

```bash
docker compose down -v
```

## Services

### Portainer

- URL: `https://localhost:9443` (recommended)
- Alternative URL: `http://localhost:9000`
- Persistent data volume: `portainer_data`

Notes:
- On first launch, Portainer asks you to create an admin user.
- Browser may show a certificate warning on HTTPS for local/dev usage.

### pgAdmin 4

- URL: `http://localhost:5050`
- Default email: `admin@admin.com`
- Default password: `admin`

Security note:
- These credentials are suitable only for local development.
- Change `PGADMIN_DEFAULT_PASSWORD` in `docker-compose.yaml` before exposing this beyond localhost.

## Networking

Both services are attached to the internal Docker network:

- `tools_network`

## Common Commands

View logs:

```bash
docker compose logs -f
```

Restart services:

```bash
docker compose restart
```

Pull newer images:

```bash
docker compose pull
```

Recreate containers after image updates:

```bash
docker compose up -d --force-recreate
```

## Troubleshooting

Port already in use:
- Update host ports in `docker-compose.yaml` (`9000`, `9443`, `5050`) and restart.

Docker socket permission issues:
- Ensure Docker Desktop is running and your user can access Docker.

Service health checks:
- Use `docker compose ps` and `docker compose logs -f <service_name>` for details.

## Optional Improvements

- Move sensitive values to a `.env` file.
- Add a persistent volume for pgAdmin data if you want saved servers/settings across restarts.
- Pin image tags to specific versions instead of using `latest`.
