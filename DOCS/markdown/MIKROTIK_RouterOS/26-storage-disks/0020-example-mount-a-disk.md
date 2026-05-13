## Example: Mount a disk 

In this example, one RouterOS device is used as a storage server ( Host ) and another RouterOS device requires a storage device to be mounted over the network ( Client ). 

1.  Use the following commands on Host : 

```
/disk set disk1 nvme-tcp-export=yes nvme-tcp-port=4420
```

2.  Use the following commands on Client : 

```
/disk add type=nvme-tcp nvme-tcp-address=192.168.1.1 nvme-tcp-name=disk1
```

3.  Your Client will now see a disk that is actually mounted over network using NVMe-Over-TCP
