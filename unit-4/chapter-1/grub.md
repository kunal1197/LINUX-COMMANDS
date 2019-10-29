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

# Grub Boot Floppy

## Change directory to the location that contains GRUB images

```console
user@programmer:~$ cd /usr/share/grub/i386-redhat/
```

## Write stage1 to first 512 byts

```console
user@programmer:~$ dd if=stage1 of=/dev/fd0 bs=512 count=1
```

## Write stage2 after the stage1

```console
user@programmer:~$ dd if=stage2 of=/dev/fd0 bs=512
```

# Installing GRUB on MBR using a GRUB Floppy

```console
grub> root (hd0, 0)
grub> setup (hd0)
```

# Adding new kernel to boot with GRUB

## Change current working directory to /boot

```console
user@programmer:~$ cd /boot
```

## Make a copy of current kernel

```console
user@programmer:~$ cp vmlinuz-2.6.25-14.fc9.i686 duplicate-kernel
```

## Make a copy of initrd image

```console
user@programmer:~$ cp initrd-2.6.25-14.fc9.i686.img duplicate-initrd.img
```

## Change in /boot/grub/menu.1st

```console
title The Duplicate Kernel
  color yellow/black
  root (hd0,0)
  kernel /duplicate-kernel ro root=UUID=7db5-4c27
  initrd /duplicate-initrd.img
```

## Create another entry to change fg and bg colors

```console
title The change color entry
  color yellow/black
```

## Comment out splashimage

## Comment out hiddenmenu

# The init process

### The various runlevels are

```console
0     Halt the system
1     Enter single-user mode
2     Multiuser mode, but without Network File System (NFS)
3     Full multiuser mode
4     Unused
5     Same as runlevel 3, except using an X Window System login  
      rather than a text based login
6     Reboot the system
```
