# General

## Useful commands

### List all mounted filesystems

```bash
cat /proc/mounts
```

### List all files changed/written since last boot

Requires: fake-hwclock

```bash
sudo find / /boot -xdev -newermt "$(cat /etc/fake-hwclock.data) UTC" -ls
```
Let's break this down:

- ``find``: This is a powerful command-line utility in Unix and Linux used to search for files and directories in a directory hierarchy. It has various options and criteria for searching.

- ``/ /boot``: These are the starting directories for the find command. In this case, it's searching in the root directory / and the /boot directory.

- ``-xdev``: This option prevents find from descending into directories on different filesystems. It ensures that the search is confined to the filesystem containing the specified starting points (/ and /boot in this case).

- ``-newermt "$(cat /etc/fake-hwclock.data) UTC"``: This part of the command specifies the time-based criterion for the search. It looks for files modified after the timestamp stored in the file /etc/fake-hwclock.data. The cat command reads the content of the file, and $(...) is used for command substitution. The timestamp is assumed to be in UTC (Coordinated Universal Time).

- ``-ls``: This option causes find to output detailed information about each file found, similar to the ls -l command. It includes information such as permissions, ownership, size, and modification time.

## Useful tools

### lsblk

lsblk is a Linux command used to list information about block devices, which includes hard drives, solid-state drives (SSDs), and other storage devices, as well as their partitions. The information provided by lsblk includes details about the size, type, and mount points of these devices.

Basic syntax:
```
lsblk
```

The output typically includes columns such as:

- **NAME**: This column shows the names of the block devices and their partitions. For example, you might see entries like sda for the first disk, sda1 for the first partition on that disk, and so on.

- **SIZE**: Indicates the size of the block device or partition in bytes, kilobytes, megabytes, etc.

- **TYPE**: Specifies the type of block device, such as disk or partition.

- **MOUNTPOINT**: Displays the mount point, if applicable. This will be empty for devices that are not currently mounted.

- **LABEL**: Shows the label assigned to the file system on the device, if any.

- **FSTYPE**: Indicates the type of file system (e.g., ext4, NTFS) present on the device.

- **MODEL**: Provides information about the device's model or make.

- **UUID**: Displays the Universally Unique Identifier associated with the device or partition.