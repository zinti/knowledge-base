# Mounting

## fstab

*File location: `/etc/fstab`*


`fstab` (File System Table) is a configuration file in Linux that defines how block devices (such as hard drives, SSDs, USB drives) and partitions are mounted into the file system. It contains information about where and how these devices should be mounted when the system starts up.

Each line in the fstab file represents a separate file system entry and follows a specific format:

```
<device> <mount_point> <fs_type> <options> <dump> <pass>
```

Here's what each field represents:

- `<device>`: Specifies the block device or partition to be mounted. This can be a device path like `/dev/sdX` or a UUID (Universally Unique Identifier) like `UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`.

- `<mount_point>`: Specifies the directory where the device will be mounted.

- `<fs_type>`: Indicates the type of file system on the device (e.g., ext4, ntfs, vfat).

- `<options>`: Defines various mount options, such as read-only or read-write access, permissions, and more.

- `<dump>`: Used by the dump backup utility. In most cases, you can set this to 0.

- `<pass>`: Used by the fsck file system check utility. In most cases, you can set this to 0.

Example:
```
# System partitions
proc                  /proc           proc    defaults             0       0
PARTUUID=07e5a64a-01  /boot           vfat    defaults,ro          0       2
PARTUUID=07e5a64a-02  /               ext4    defaults,noatime,ro  0       1
PARTUUID=07e5a64a-03  /home           ext4    defaults,noatime,rw  0       0

# Tmpfs for read-only filesystem
tmpfs                 /tmp            tmpfs   nodev,nosuid         0       0
tmpfs                 /var/log        tmpfs   nodev,nosuid         0       0
tmpfs                 /var/tmp        tmpfs   nodev,nosuid         0       0
tmpfs                 /var/cache      tmpfs   nodev,nosuid         0       0

# Removable Devices
LABEL=usb256     /media/usb256      auto     nofail,x-systemd.device-timeout=15     0    0
LABEL=usb128     /media/usb128      auto     nofail,x-systemd.device-timeout=15     0    0

```
