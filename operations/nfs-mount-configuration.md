# NFS Mount Configuration

## Objective

Configure persistent NFS mount from Ubuntu host to Synology NAS.

## NFS Service Validation

Check NFS port availability:

nc -zv 192.168.1.126 2049

If connection is refused:
- Enable NFS service in Synology DSM
- Confirm shared folder permissions allow host IP access

## Manual Mount Test

sudo mount -t nfs 192.168.1.126:/volume1/media /mnt/media

Verify mount:

df -h /mnt/media
mount | grep /mnt/media

## Persistent Mount Configuration

Edit /etc/fstab:

sudo nano /etc/fstab

Add:

192.168.1.126:/volume1/media /mnt/media nfs defaults,_netdev 0 0

Explanation:
- defaults → standard mount options
- _netdev → delays mount until network is available
- 0 0 → disable dump and fsck checks

## Validation

Reboot system:

sudo reboot

After reboot:

mount | grep /mnt/media

If mount persists successfully, configuration is complete.
