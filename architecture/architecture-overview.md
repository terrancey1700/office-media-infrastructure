# Architecture Overview

## High-Level Design

Compute Layer:
- Ubuntu 24.04 host
- Docker containerized arr-stack (Plex, Sonarr, Radarr, qBittorrent)

Storage Layer:
- Synology DSM (SHR – 1 drive fault tolerance)
- NFS mounted to Ubuntu host
- Persistent mount via /etc/fstab with _netdev option

Networking:
- UniFi-based local network
- Tailscale for secure remote access
- NFSv3 over TCP for storage communication

Data Flow:

qBittorrent → /mnt/media/downloads  
Sonarr/Radarr → organize to /mnt/media/tv and /mnt/media/movies  
Plex → reads from NAS via NFS mount  

## Storage Strategy

- Primary storage: Synology SHR volume
- Snapshot retention policy enabled
- Local external disk retained temporarily (Toshiba 2TB)
- Future plan: Offsite backup integration
