# To back up MBR (Master Boot Record):-

```console
user@programmer:~$ dd if=/dev/sda of=/tmp/COPY_OF_MBR bs=512 count = 1
```

# Creating a boot rescue disk

## Generate ISO image

```console
user@programmer:~$ mkbootdisk --device /tmp/BOOT-CD.iso --iso `uname -r`
```

## Burn the ISO into CD

```console
user@programmer:~$ cdrecord speed=4 -eject --dev=/dev/sr0 /tmp/BOOT-CD.iso
```

# Installing GRUB from the GRUB shell

## Launch GRUB's shell

```console
user@programmer:~$ grub
```

## Set GRUB's root device from default fd0 to hd0

```console
user@programmer:~$ root (hd0, 0)
```

## Find the stage1 image

```console
user@programmer:~$ find /grub/stage1
```

## Install the GRUB bootloader directly on MBR

```console
user@programmer:~$ setup (hd0)
```

## Quit the GRUB shell

```console
user@programmer:~$ quit
```
