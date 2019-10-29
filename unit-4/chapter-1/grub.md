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
