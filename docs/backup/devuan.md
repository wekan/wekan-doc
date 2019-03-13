# Backup / Restore with Debian OFT package

## Configuration

!!! warning
    You must configure the `BACKUP_DIR` variable into the `/etc/wekan/wekan-oft-0` to indicate the directory where to dump the wekan datas.

## Backup

```shell
/etc/init.d/wekan-oft-0 data backup
```

## Restore

```shell
/etc/init.d/wekan-oft-0 data restore
```

