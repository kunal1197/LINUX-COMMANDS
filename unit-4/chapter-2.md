# Mount using mount command

```console
user@programmer:~$ mount -o ro /dev/hda3 /bogus-directory
```

# Unmounting file systems

```console
user@programmer:~$ umount /bogus-directory
```

# Running fsck command

## Unmount

```console
user@programmer:~$ umount /home
```

## Run fsck

```console
user@programmer:~$ fsck /dev/mapper/VolGroup00-Logvol02
```

## Forcefully check that fs is marked clean

```console
user@programmer:~$ fsck.ext3 -f -y /dev/mapper/VolGroup00-Logvol02
```

# Creating a partition

## List current partition table

```console
user@programmer:~$ fdisk -l /dev/sda
```

## Repartitioning

```console
user@programmer:~$ fdisk /dev/sda
```

### Note: In the fdisk utility press 'm' for help

## Print the partition table

```console
Command: p
```

## Create a new partition

```console
Command: n
```

## Select primary partition type

```console
p
```

## Select partition number

```console
Partition number: 3
```

## Specify partition size

```console
First cylinder: 1201
Last cylinder: 1305
```

## Change the partition type

```console
Command: t
```

## Choose the partition

```console
Partition number: 3
```

## Select partition type

```console
Hex code: 8e
```

## Commit the changes

```console
Command: w
```

## Quit the fdisk utility

```console
Command: q
```

## Reboot the system

```console
user@programmer:~$ reboot
```

# Create a physical volume

## Display all physical volumes

```console
user@programmer:~$ pvdisplay
```

## Create a new physical volume

### Note:- This physical volume is created using the newly created partition.

```console
user@programmer:~$ pvcreate /dev/sda3
```

# Adding a physical group to a volume group

## Display all volume groups

```console
user@programmer:~$ vgdisplay
```

## Assign the physical volume to volume group

```console
user@programmer:~$ vgextend VolGroup00 /dev/sda3
```

# Create a logical volume

## View all the LVs

```console
user@programmer:~$ lvdisplay | less
```

## Create a new LV (physical extents)

```console
user@programmer:~$ lvcreate -l 26 --name LogVol04 VolGroup00
```

## Create a new LV (size)

```console
user@programmer:~$ lvcreate -L 864M --name LogVol04 VolGroup00
```

# Creating file systems

## Create a file system (ext3)

```console
user@programmer:~$ mkfs.ext3 /dev/VolGroup00/LogVol04
```

## Create a mount point

```console
user@programmer:~$ mkdir /new_var
```

## Mount (temporarily)

```console
user@programmer:~$ mount /dev/VolGroup00/LogVol04 /new_var
```

# Copy content from /var to /new_var

```console
user@programmer:~$ cp -rp /var/* /new_var/
```

## Safety measures

```console
user@programmer:~$ mount --bind /var/lib/nfs/rpc_pipefs \
/new_var/lib/nfs/rpc_pipefs
```

## Rename /var to /old_var

```console
user@programmer:~$ mv /var /old_var
```

## Create a new empty /var

```console
user@programmer:~$ mkdir /var
```

# Restore security contexts

```console
user@programmer:~$ restorecon -R /var
```

## Create an entry in /etc/fstab (for permanent mounting)

```console
user@programmer:~$ echo "/dev/VolGroup00/LogVol04 /var ext3 defaults 1 2" >> /etc/fstab
```

## Reboot the system

```console
user@programmer:~$ shutdown -r now
```

## After the system boots up delete /old_var and /new_var
