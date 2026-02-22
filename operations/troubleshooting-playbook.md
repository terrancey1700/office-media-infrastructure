# Infrastructure Troubleshooting Playbook

## Philosophy

Troubleshoot from the bottom of the stack upward:

Hardware → OS → Network → Storage → Services → Application

Never assume. Validate each layer.

---

## Disk & Storage Issues

Check disk usage:

df -h

Check block devices:

lsblk

Check mount status:

mount | grep /mnt/media

Check directory usage:

du -sh /mnt/media/*

Common issues:
- Root filesystem full
- Incorrect mount point
- NFS not mounted after reboot

Resolution pattern:
1. Confirm mount
2. Confirm free space
3. Confirm correct path mapping in Docker

---

## NFS Connectivity Issues

Test port availability:

nc -zv 192.168.1.126 2049

If connection refused:
- Confirm NFS service enabled in DSM
- Verify shared folder permissions
- Validate firewall rules

Check mount version:

mount | grep nfs

---

## Docker & Container Issues

Check running containers:

docker ps

Check container logs:

docker logs plex

Restart container:

docker restart plex

Validate bind mounts:

docker inspect plex | grep Mounts -A 20

Common issues:
- Incorrect volume mapping
- Permission mismatch
- Service running but path incorrect

---

## Network Connectivity

Test connectivity:

ping 192.168.1.126

Test service endpoint:

curl http://localhost:32400/web

Validate Tailscale status:

tailscale status

---

## Migration Validation

Confirm rsync completion:

Look for:
to-chk=0

Compare source and destination size:

du -sh /mnt/media
du -sh /mnt/media_new

---

## Reboot Validation Checklist

After reboot:

1. mount | grep /mnt/media
2. docker ps
3. Access Plex UI
4. Confirm snapshot schedule still active

---

## Root Cause Patterns Observed

- Services appeared online but storage mount failed
- NFS protocol mismatch errors
- SSH tunnel confusion when remote
- Disk space exhaustion caused service instability

Resolution approach:
- Isolate layer
- Validate assumptions
- Test incrementally
- Avoid changing multiple variables simultaneously
