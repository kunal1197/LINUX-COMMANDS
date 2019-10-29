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

### The various runlevels are, these are specified in /etc/inittab

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

# Creating carpald.sh Script

### Note:- This script prompts user to take a break every 1 hour. Name of the file: carparld.sh

## Open text editor and type the following

```console
#!/bin/bash
#Description: This is a prompt to tell user to take a break
every 1 hour.

ADDR=root@localhost
while true
do
  sleep 1h
  echo "Get up and take a break" | \
  mail -s "Warning! Get up!" $ADDR
done
```

## Save and change permissions

```console
user@programmer:~$ chmod 755 carpald.sh
```

## Move the script to /usr/local/sbin

```console
user@programmer:~$ mv carpald.sh /usr/local/sbin/
```

# Creating the Startup Script

## Open text editor and type the following

```console
#!/bin/sh
#Carpal
#chkconfig 35 99 01
# description: This is a prompt to tell user to take a break
every 1 hr.

# Source function library
. /etc/rc.d/init.d/functions
[ -f /usr/local/sbin/carpald.sh ] || exit 0

case "$1" in
start)
  echo "Starting carpald: "
  /usr/local/sbin/carpald.sh &
  echo "done"
  touch /var/lock/subsys/carparld
;;
stop)
  echo -n "Stopping carpald services: "
  echo "done"
  killall -q -9 carparld &
  rm -f /var/lock/subsys/carpald
;;
status)
  status carpald
;;
restart|reload)
  $0 stop
  $0 start
;;
*)
  echo "Usage: carpald start|stop|status|restart|reload"
  exit 1
  esac
exit 0
```

### chkconfig 35 99 01 means 35 means create entries in 3 and 5 run levels, 99 means start the last and 01 means end the first.

## Save the text into file called carpald

## Change the permissions of this file

```console
user@programmer:~$ chmod 755 carpald
```

## Move into /etc/rc.d/init.d

```console
user@programmer:~$ mv carpald /etc/rc.d/init.d
```

## Tell chkconfig of existence of this script

```console
user@programmer:~$ chkconfig --add carpald
```

## Check the service

```console
user@programmer:~$ service carpald status
user@programmer:~$ service carpald start
user@programmer:~$ service carpald stop
```

# Enabling and disabling services

## View all runlevels in carpald.sh

```console
user@programmer:~$ chkconfig --list carpald
```

## Make carpald.sh start up automatically at run level 2

```console
user@programmer:~$ chkconfig --level 2 carpald on
```

# Disabling a service

## Disable the program

```console
user@programmer:~$ chkconfig carpald off
```

## Delete the program

```console
user@programmer:~$ chkconfig --del carpald
user@programmer:~$ rm -f /usr/local/sbin/carpald.sh
```
