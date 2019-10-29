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
