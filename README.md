# Office Media Infrastructure Deployment

End-to-end small-business media infrastructure deployment using Ubuntu, Docker, NFS, Synology SHR, and Tailscale. Includes live storage migration and production hardening.

---

# Executive Summary

## Situation

The office required a private, business-hosted media infrastructure capable of supporting 3–5 concurrent remote Plex users while maintaining network performance, redundancy, and scalability.

Initial state:

- `Media stored on local external disk`
- `No redundancy`
- `No snapshot protection`
- `Compute and storage tightly coupled`
- `No persistent network mount`
- `No production hardening`

This created operational risk and limited scalability.

---

### Task

Design and deploy a production-stable infrastructure that:

- `Separates compute and storage`
- `Implements redundant storage (SHR)`
- `Automates media acquisition`
- `Enables secure remote access`
- `Survives reboot`
- `Is operationally documented`

---

## Action

### Phase 1 – Planning & Architecture

- Designed UniFi-based network topology
- Modeled ISP upload capacity for concurrent streaming
- Selected Synology SHR (1-drive fault tolerance)
- Designed arr-stack container architecture
- Defined media and automation directory structure


### Phase 2 – Deployment & Operationalization

- Installed Ubuntu Server on Lenovo ThinkCentre
- Installed Docker and Docker Compose
- Deployed arr-stack (Sonarr, Radarr, Prowlarr, qBittorrent, FlareSolverr, Plex)
- Configured end-to-end automation pipeline
- Installed Tailscale for secure overlay networking
- Validated remote SSH and Plex access

### Phase 3 – Migration, Persistence & Hardening

- Mounted Synology via NFS
- Migrated ~1.1TB using rsync with metadata preservation
- Performed controlled cutover
- Configured persistent mount in /etc/fstab
- Verified mount survival across reboot
- Enabled Snapshot Replication
- Removed legacy external storage from production path


## Result

The final system is:

- `Redundant (SHR fault tolerance)`
- `Persistent across reboots`
- `Fully automated`
- `Secure (no public port forwarding)`
- `Remotely manageable`
- `Architecturally separated`
- `Production-stable`


## Technologies Used

- Ubuntu Server 24.04
- Docker & Docker Compose
- Synology DSM (SHR)
- NFS
- rsync
- tmux
- Tailscale
- UniFi Network Stack
- Linux system tools (df, lsblk, mount, fstab)

## Architecture Overview

- User → Tailscale → Lenovo (Docker Host) → NFS → Synology (SHR Storage)


### Detailed documentation:

- `ARCHITECTURE.md`
- `RUNBOOK.md`
- `TROUBLESHOOTING.md`
- `PROJECT_PHASES.md`
- `Skills Demonstrated`
- `Linux system administration`
- `Persistent NFS configuration`
- `Data migration with rsync`
- `Docker container lifecycle management`
- `Log-based debugging`
- `Network validation and capacity modeling`
- `Storage redundancy planning`
- `Risk mitigation and hardening`
- `Infrastructure documentation`

## Future Improvements

- Hyper Backup automation
- Offsite backup strategy
- Monitoring stack (Prometheus + Grafana)
- SSH key-only enforcement
- Firewall tightening
- UPS graceful shutdown integration
- Infrastructure automation via Ansible
- Replace README with full project documentation


---

## Skills Demonstrated

- Linux systems administration
- Docker containerization
- NFS network storage
- Synology SHR storage architecture
- Live data migration using rsync
- Snapshot retention policy design
- VPN-based remote access (Tailscale)
- Troubleshooting methodology
- Infrastructure documentation

---

## Author

Terrance Young  
Aspiring DevOps / Systems Engineer
