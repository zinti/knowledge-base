# File System and Volumes

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

## fdisk

The fdisk tool in Linux is a command-line utility used for disk partitioning. It allows users to create, delete, and manage partitions on a hard disk. fdisk is a powerful tool that is often used to set up the partition table on a new disk or to reconfigure existing partitions.

- Creating Partitions: fdisk allows you to create new partitions on a disk. You can specify the type of partition (e.g., primary or extended) and the size.

- Deleting Partitions: You can use fdisk to remove existing partitions from a disk. Be careful when deleting partitions, as it can result in data loss.

- Changing Partition Type: fdisk allows you to change the type of a partition, which can be useful if you want to convert a partition from one type to another (e.g., from primary to extended).

- Displaying Partition Information: You can use fdisk to display information about the partitions on a disk, including their sizes, types, and start/end sectors.

- Setting Bootable Partitions: You can mark a partition as bootable using fdisk. This is important for the boot process on the disk.

- Writing Changes to Disk: After you make changes to the partition table, you need to write the changes to the disk for them to take effect.

Keep in mind that there are other partitioning tools available in Linux, such as parted and gparted, which provide more user-friendly interfaces and additional features compared to fdisk.

## Format file-system

### mkfs.ext4

mkfs.ext4 is a Linux command used to create a new ext4 file system on a storage device, such as a hard drive or a partition. The ext4 file system is a widely used file system in Linux distributions due to its performance, reliability, and compatibility with earlier ext file systems.

Basic syntax:
```bash
sudo mkfs.ext4 -E lazy_itable_init=0,lazy_journal_init=0 -L my_usb_lable /path/to/partition
```

Options:
- -E lazy_itable_init, lazy_journal_init: Format takes longer but later no more resources needed to init the inodes
- -L <lable>: define a lable

Example:
```bash
sudo mkfs.ext4 -E lazy_itable_init=0,lazy_journal_init=0 -L my_usb_stick /dev/sdb1
```

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
