# Poor Man's Backup

Backup a folder to the local filesystem with periodic rotating backups, based on [prodrigestivill/docker-postgres-backup-local](https://github.com/prodrigestivill/docker-postgres-backup-local/).

Supports the following Docker architectures: `linux/amd64`, `linux/arm64`.

## Usage

Docker:

```sh
docker run -e PMB__SOURCE=/tmp/source -e PMB__DESTINATION=/tmp/destination ghcr.io/bjw-s/pmb:rolling
```

### Environment Variables

| env variable | description |default|
|--|--|--|
| PMB__SOURCE | Source directory to backup. | `**None**` |
| PMB__DESTINATION | Destination directory to save the backup to. | `**None**` |
| PMB__KEEP_DAYS | Number of daily backups to keep before removal. | `7` |
| PMB__CRON_HEALTHCHECK_PORT | Port listening for cron-schedule health check. | `18080` |
| PMB__CRON_SCHEDULE | [Cron-schedule](http://godoc.org/github.com/robfig/cron#hdr-Predefined_schedules) specifying the interval between backups. If set to empty the backup command will run just once. | `@daily` |
| TZ | [POSIX TZ variable](https://www.gnu.org/software/libc/manual/html_node/TZ-Variable.html) specifying the timezone used to evaluate SCHEDULE cron (example "Europe/Paris"). | `""` |

### Automatic Periodic Backups

You can change the `PMB__CRON_SCHEDULE` environment variable in `-e PMB__CRON_SCHEDULE="@daily"` to alter the default frequency. Default is `daily`.

More information about the scheduling can be found [here](http://godoc.org/github.com/robfig/cron#hdr-Predefined_schedules).

Folders `daily`, `weekly` and `monthly` are created and populated using hard links to save disk space.
