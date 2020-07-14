# Create cloud-init disk
```
genisoimage -o cloud-init.iso -V cidata -r -J user-data meta-data
```

# Create qcow2 disk backed by cloud img disk
```
qemu-img create -f qcow2 -o backing_file=../<cloud-image-disk> disk.qcow2 +20G
```

# Install VM
```
virt-install -n <name> --memory 4096 --import --disk path=disk.qcow2,device=disk --disk path=cloud-init.iso,device=cdrom --nographics -w network=<network-name> --os-type=generic --os-variant=<os-variant>
```
