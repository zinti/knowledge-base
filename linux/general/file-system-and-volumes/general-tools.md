# General tools

## lsblk

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