# Hardware & Storage Specification (`ronfnas`)

## Core System Specs
- **Processor / SoC:** Rockchip RK3588 (ARM64)
- **Memory:** 16GB RAM
- **Hostname:** `ronfnas`
- **Local IP:** `192.168.254.120`
- **Management Layer:** OpenMediaVault (OMV) / Docker Engine

## Storage & ZFS Topology
Global setting: `atime=off` across all datasets to minimize metadata write amplification.

| Dataset Path | Record Size | Purpose / Workload |
| :--- | :--- | :--- |
| `tank/appdata-32K` | 32K | Optimized for small files (Caddy data, caches, thumbs, profiles) |
| `tank/immich` | 1M | High-capacity storage for media assets (`library/`, `upload/`, `encoded-video/`) |
| `tank/db-zones` | 32K | High-performance transactional storage for Postgres database files |
| `tank/backups` | Default | Isolated storage for automated database `.sql.gz` dump archives |
| `tank/files` & `tank/media` | 1M | Broad streaming media and general file storage |

## NVMe Pool Configuration
- **Disks:** 4x SP002TBP34A60M28 NVMe drives
- **Layout:** ZFS RAIDZ1 (`Z1`)
- **Record Size:** 8M pool-level default with dataset-specific overrides (above)
