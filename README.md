# My Docker Container

This repository contains several docker-compose setups used for local development. The table below lists each service, the compose file location, a suggested/default port (these can be changed in the compose files) and a quick local URL you can try.

| Service                             | compose file path                      | suggested port(s)                     | Local URL (suggested)             |
| ----------------------------------- | -------------------------------------- | ------------------------------------- | --------------------------------- |
| Airflow (web UI)                    | `airflow/docker-compose.yaml`          | 8080 (webserver)                      | <http://localhost:8080>             |
| CouchDB                             | `CouchDB/docker-compose.yaml`          | 5984                                  | <http://localhost:5984>             |
| Jenkins                             | `jenkins/docker-compose.yml`           | 8080                                  | <http://localhost:8080>             |
| n8n                                 | `n8n/docker-compose.yaml`              | 5678                                  | <http://localhost:5678>             |
| Ollama (model server)               | `ollama/docker-compose.yaml`           | 11434                                 | <http://localhost:11434>            |
| Postgres + pgAdmin                  | `postgres_pgadmin/docker-compose.yaml` | Postgres: 5432, pgAdmin: 8086         | <http://localhost:8086>             |
| Qdrant (vector DB)                  | `qdrant_vecterDB/docker-compose.yaml`  | 6333                                  | <http://localhost:6333>             |
| Traefik (reverse proxy / dashboard) | `traefik/docker-compose.yml`           | Dashboard: 8080; HTTP: 80; HTTPS: 443 | <http://localhost:8080> (dashboard) |
| Traefik proxy (alternate)           | `traefik_proxy/docker-compose.yaml`    | depends on config                     | see compose file                  |

Notes:

- The "suggested ports" are common defaults. Your compose files may map different host ports — always verify before relying on a URL.
- There may be other service folders in this repo. Check the folder names for additional compose files.

Quick commands (run from the repo root):

```zsh
# Show which ports a compose project exposes (for a specific compose file):
docker compose -f <path/to/docker-compose.yml> ps

# Or run this to see all running containers and their host port mappings:
docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Ports}}"

# Start a specific compose stack (detached):
docker compose -f <path/to/docker-compose.yml> up -d

# Bring down a stack and remove volumes (be careful):
docker compose -f <path/to/docker-compose.yml> down -v
```

Troubleshooting / tips:

- If a port is already in use, change the host port in the corresponding compose file (left side of the mapping, e.g. "8086:80").
- If you want a single entrypoint for all services, configure `traefik` to route hostnames/paths to each service and expose traefik's ports (80/443).
- To inspect a service's logs:

```zsh
docker compose -f <path/to/docker-compose.yml> logs -f <service_name>
```

If you'd like, I can:

- read the compose files and fill in the exact host port mappings in this README, or
- add short startup scripts to bring up the most-used stacks with one command.
