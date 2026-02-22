# Snapshot Retention Policy – Synology DSM

## Objective

Protect media storage against accidental deletion, corruption, or ransomware
using scheduled snapshot retention.

## Configuration Location

DSM → Snapshot Replication → Snapshots → Settings

## Snapshot Schedule

- Enabled daily snapshots
- First snapshot: 00:00
- Frequency: Once per day
- Applied to primary media volume

## Retention Policy (Smart Retention)

Configured rules:

- Keep all snapshots for 1 day
- Keep latest snapshot of the hour for 24 hours
- Keep latest snapshot of the day for 7 days
- Keep latest snapshot of the week for 4 weeks
- Keep latest snapshot of the month for 1 month
- Ensure minimum of 5 recent snapshots retained

## Design Considerations

- Protect against accidental file deletion
- Provide short-term rollback capability
- Limit long-term storage overhead
- Balance retention with 16TB capacity constraints

## Validation

- Confirm snapshot creation via DSM dashboard
- Verify snapshot count under Snapshot Replication
- Monitor storage usage impact

## Future Improvements

- Enable offsite replication
- Implement Hyper Backup to secondary storage
- Add ransomware detection alerts
