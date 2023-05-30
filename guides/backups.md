# Backups

Lynx has basic support for backing up your links.&#x20;

On a crontab schedule it will back up **all** of your links to a set directory, keeping the last x backups.

If a backup limit of 1 is specified the backup file will be located at `/backups/backup.json`.&#x20;

If more than one backup is specified the current ISO date will be appended to the filename, such as `/backups/backup-2023-05-30T16-30-49.991Z.json`

You can enable and configure these backups with [environment variables](../installation/environment-variables.md#backups).
