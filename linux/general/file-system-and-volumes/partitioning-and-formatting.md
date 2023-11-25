# Partitioning and formatting

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