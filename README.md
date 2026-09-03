# Infrastructure Repository (`lab`)

This repository contains the declarative infrastructure manifests, Docker Compose configurations, and automation scripts for the `ronfnas` environment.

## Architecture Overview
- **Host OS:** OpenMediaVault (OMV) on ARM64 (`RK3588`, 16GB RAM)
- **Container Engine:** Docker with Native Compose Plugin
- **Storage Backend:** ZFS pools (`tank`) with optimized record sizes per workload
- **Reverse Proxy:** Caddy handling automatic TLS via DuckDNS (`ronfnas.duckdns.org`)

## Management Workflow (GitOps-Lite)
Routine fleet maintenance is automated via the root-level `Makefile`:

- `make pull` — Pulls the latest container images for all services.
- `make up` — Deploys or updates all services in detached mode (`docker compose up -d`).
- `make down` — Stops all active container stacks.
- `make status` — Outputs the current health and status of all running containers (`docker ps -a`).

For deep troubleshooting or single-stack adjustments, navigate to the individual service directory (e.g., `cd immich/`) and run `docker compose` commands locally.
