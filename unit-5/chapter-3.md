# KVM Example

## Install virtualization package group (python-virtinst, kvm qemu, virt-manager, virt-viewer)

```console
user@programmer:~$ yum groupinstall 'Virtualization'
```

## Start libvirtd service

```console
user@programmer:~$ service libvirtd start
```

## Make sure libvirtd starts on next boot automatically

```console
user@programmer:~$ chkconfig libvirtd on
```

## Check if virtualization is enabled and running properly

```console
user@programmer:~$ virsh -c qemu:///system list
```

## Create a folder for Fedora VM

```console
user@programmer:~$ mkdir -p /home/vms/fedora-VM/
```

## Setup virtual machine using virt-install

```console
user@programmer:~$ virt-install --hvm
```

### Set the name of VM

```console
What is the name of your virtual machine? fedora-VM
```

### Set RAM size

```console
How much RAM should be allocated (in megabytes)? 1000
```

### Location to store disk image

```console
Where would you like to use as the disk (file path)?
/home/vms/fedora-VM/fedora-VM-disk.img
```

### Virtual disk size

```console
How large would you like the disk (/home/vms/fedora-VM/fedora-VM-disk) to
be (in gigabytes)? 10
```

### Enable graphic support for the VM

```console
Would you like to enable graphics support? (yes or no) yes
```

### Physical optical drive

```console
What is the virutal CD image, CD device or install location?
/dev/sr0
```
