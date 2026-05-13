## Example: Mount a file as a block device 

In this example, one RouterOS device is used as a storage server ( Host ) and another RouterOS device requires a storage device to be mounted over the network ( Client ). 

**==> picture [13 x 13] intentionally omitted <==**

Such a setup is useful when you don't want to delegate the whole disk to a Client , but rather give a fraction of the disk size to the Client . Mounting a file rather a disk is going to have a lower performance than mounting a disk (or partition) using NVMe-Over-TCP. 

1.   Use the following commands on Host to create a file that is going to be used as a block device: 

```
/disk add type=file file-path=disk1/BIGFILE.img file-size=10G slot=blockdevice1
/disk set blockdevice1 nvme-tcp-export=yes
```

2.  Use the following commands on Client to mount the file as a block device: 

```
/disk nvme-discover 192.168.1.1
/disk add nvme-tcp-address=192.168.1.1 nvme-tcp-name=blockdevice1 type=nvme-tcp
/disk format blockdevice1 file-system=ext4
```

3.  Your Client will now see a new disk called `blockdevice1` even though on the Server the storage device is actually a file. 

**==> picture [13 x 13] intentionally omitted <==**

In case you want to mount the block device on a Linux Client , then check the LinuxClient section. 

1671
