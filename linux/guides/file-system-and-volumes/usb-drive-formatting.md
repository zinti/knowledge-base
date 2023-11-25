# Format a USB Drive

## Step 1: Identifying the USB drive

We should first figure out the block device that’s mapped to our actual physical USB drive.
For that purpose, we’ll use the lsblk utility:

```bash
lsblk
```

Example output:
```
NAME   MAJ:MIN RM  SIZE    RO TYPE MOUNTPOINT
sda      8:0    0  500G    0 disk 
└─sda1   8:1    0  500G    0 part /
sdb      8:16   1  116.6G  0 disk 
└─sdb1   8:17   1  116.6G  0 part /media/usb_drive
```

Here, we are interested in the `/dev/sdb` block device, which is mapped to a 128 GB USB drive.

If it's mounted (/media/usb_drive in this example), unmount it using:
```bash
sudo umount /dev/sdb1
```

## Step 2: Creating the Partition

We use the fdisk utility for creating the partition. Open the partitioning tool for the specified device (/dev/sdb in this example):

```bash
sudo fdisk /dev/sdb
```

Create a new GPT (GUID Partition Table) schema by typing in "g":

```bash
Command (m for help): g
Created a new GPT disklabel (GUID: 2561EC1C-0F35-5547-9541-BCB0762B75B1).
```

We can now create a new partition on it by typing in "n" and entering the default values (just hit enter):

```bash
Command (m for help): n
Partition number (1-128, default 1):
First sector (2048-244457438, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-244457438, default 244457438):

Created a new partition 1 of type 'Linux filesystem' and of size 116.6 GiB.
```

> **_Remark:_** We created now 1 partition over the whole block device. If you want to create 2 partitions or more, use the sectors to specify the start and end point of the partition.

Check the current partition table by entering "p":
```bash
Command (m for help): p
Disk /dev/sdb: 116.57 GiB, 125162225664 bytes, 244457472 sectors
Disk model: SanDisk 3.2 Gen1
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 2561EC1C-0F35-5547-9541-BCB0762B75B1

Device     Start       End   Sectors   Size Type
/dev/sdb1   2048 244457438 244455391 116.6G Linux filesystem
```
You see, that we created 1 partition (dev/sdb1) over the whole disk.

Now, we’ll write the changes to our USB drive by entering "w":
```bash
Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

## Step 3: Formatting the Partition

In Linux, we can use a variety of different file systems. Each file system has its own unique set of utilities. For example, we can use the mkfs.ext4 utility to create a new ext4 file system on a partition.

### ext4

On Linux, we can create and format a partition as ext4 (Extended File System) using the mkfs.ext4 utility.

Let’s create and format the file system on /dev/sdb1:
```bash
sudo mkfs.ext4 -E lazy_itable_init=0,lazy_journal_init=0 -L MyUsbDrive /dev/sdb1
```
Let’s break this down:
- ``-E lazy_itable_init=0,lazy_journal_init=0``: Disabling lazy initialization can result in a longer formatting process, but it ensures that all critical components are fully initialized at the time of formatting, potentially reducing the time it takes to mount the filesystem later.
- ``-L MyUsbDrive``: Specifies the label for the partition

Once we run the command, it wipes out the existing data and creates a new ext4 partition on the disk.


## Step 4 (optional): Wiping Data From the USB Drive

When we format a drive, it doesn’t necessarily erase all the data. Indeed, it does change the file system structures. However, some data could remain recoverable.

For that purpose, we can overwrite the existing data with zeroes or random garbage to ensure that the data remains unrecoverable. For this purpose, we can use for example the tool dd:

```bash
sudo dd if=/dev/zero of=/dev/sdb1 status=progress
```

