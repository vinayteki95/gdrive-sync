# gdrive-sync

## Syncronize Directories ( Google Drive <> Linux Machine )
 - rclone ( remote cloning tool )
 - cron   ( linux scheduler )

## Current Setup
 - Permissions: execute permissions to "start" script
    - `chmod +x start`
 - rclone has to be configured manually for now (https://rclone.org/drive/)
    - Basic installation of rclone is taken care off, when `SKIP_RCLONE_SETUP="no"` parameter is set
 - Synchronization script is scheduled using linux cron (` sudo crontab -e `)
    - `0 18 * * * /home/fr33b1rd/SystemManagement/gdrive-sync/start  > /var/log/cron/gdrive-sync.log 2>&1`
 - Cron logs flow into syslog (linux defaults)
    - `tail -f -n 20 /var/log/syslog | grep CRON`
 - Script logs flow into /var/log/cron/gdrive-sync.log
    - `cat /var/log/cron/gdrive-sync.log`
    - currently these logs are being overwritten to save storage (For appending logs - use '>>' in place of '>')
        - `0 18 * * * /home/fr33b1rd/SystemManagement/gdrive-sync/start  >> /var/log/cron/gdrive-sync.log 2>&1`

## TO-DO
 - seperate configuration file for parameters
 - multiple synchronization folders
 - better log management
 - multiple syncronization patterns
    - sync local to remote
    - sync remote to local
    - sync local to remote and remote to local for redundancy
        - deletion has to be done manually in both locations
 - Non root execution
 - Command line arguments for simple operational changes
 - Better documentation once the features grow
