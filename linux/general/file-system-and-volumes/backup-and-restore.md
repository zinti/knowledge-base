# Backup and restore

## Backup volume (dd)

Basic syntax:
```bash
sudo dd if=/path/to/volume/or/partition of=/path/to/image.img status=progress
```

Options:
- count: Backup until given sector

Example:
```bash
sudo dd if=/dev/sdb of=~/my_backup.img status=progress
```

### Zip Backup

Syntax:
```bash
gzip my_backup.img
```

-> Creates my_backup.img.gz

## Restore Backup (dd)

Basic syntax:
```bash
sudo dd if=<path_to_image.img> dd=<path_to_device> status=progress conv=sync
```

Example:
```bash
sudo dd if=~/my_backup.img of=/dev/sdb status=progress conv=sync
```
