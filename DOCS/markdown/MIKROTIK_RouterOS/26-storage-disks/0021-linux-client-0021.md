## Linux Client 

Use these commands to setup NVM-Over-TCP on a Linux Client . 

1.  Load kernel module 

```
modprobe nvme_tcp
```

2.  Discover existing NVMe-Over-TCP mounts: 

```
nvme discover -t tcp -a 192.168.1.1 -s 4420
```

1670 

```
#OUTPUT:
Discovery Log Number of Records 1, Generation counter 2
=====Discovery Log Entry 0======
trtype:  tcp
adrfam:  ipv4
subtype: nvme subsystem
treq:    not specified, sq flow control disable supported
portid:  4420
trsvcid: 4420
subnqn:  disk1
traddr:  10.155.166.7
sectype: none
```

3.  Connect to the NVMe-Over-TCP mount: 

```
nvme connect -t tcp -a 192.168.1.1 -s 4420 -n disk1
```

4.  Block devices now should be available: 

```
ls /dev/nvme*
```

```
#OUTPUT:
/dev/nvme0  /dev/nvme0n1  /dev/nvme-fabrics
```

5.  You can now use the mounted block device as any other block device on your Linux Client 

. 

In case you want to disconnect the mounted block device: 

```
nvme disconnect -d /dev/nvme0
```
