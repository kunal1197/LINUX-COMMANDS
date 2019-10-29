# To back up MBR (Master Boot Record):-

```console
user@programmer:~$ dd if=/dev/sda of=/tmp/COPY_OF_MBR bs=512 count = 1
```

# Creating a boot rescue disk
