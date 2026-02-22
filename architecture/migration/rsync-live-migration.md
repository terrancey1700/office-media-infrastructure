# Live Storage Migration – Local Disk to Synology NAS

## Objective

Migrate ~1.5TB of media from local external disk (/mnt/media on Toshiba 2TB)
to Synology SHR storage mounted via NFS.

## Initial State

- Local ext4 disk mounted at /mnt/media
- No persistent NFS mount
- Services dependent on local storage
- Production Plex usage active

## Migration Strategy

1. Mount NAS via NFS:
   sudo mount -t nfs 192.168.1.126:/volume1/media /mnt/media_new

2. Validate mount:
   df -h /mnt/media_new

3. Perform live rsync inside tmux:

   tmux new -s migration

   sudo rsync -aHAXv --numeric-ids --info=progress2 \
   /mnt/media/ /mnt/media_new/

4. Validate transfer completion:
   Check "to-chk=0" and compare total size.

5. Update mount configuration:
   Replace local disk mount with NFS mount in /etc/fstab:

   192.168.1.126:/volume1/media /mnt/media nfs defaults,_netdev 0 0

6. Reboot test to confirm persistent mount.

## Issues Encountered

- NFS port 2049 initially refused (service not enabled)
- Protocol mismatch errors
- Root filesystem filled during earlier transfer attempt
- SSH tunneling confusion when remote

## Solutions

- Enabled NFS service on Synology DSM
- Verified connectivity using nc -zv 192.168.1.126 2049
- Cleaned incorrect mount points
- Used tmux to prevent interruption during SSH disconnect
- Validated final mount using:

  mount | grep /mnt/media

## Result

- 1.5TB successfully migrated
- Services now reading directly from NAS
- Persistent NFS mount configured
- System survives reboot
