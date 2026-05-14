## Example: Mount a RAID array 

In this example, one RouterOS device is used as a storage server ( Host ) and another RouterOS device requires a storage device to be mounted over the network ( Client ), but also provides data redundancy. 

1.  Setup a RAID on the Host , for example: 

```
/disk add raid-device-count=8 raid-type=6 slot=RAID6_array type=raid
/disk set disk1 raid-master=RAID6_array raid-role=0
/disk set disk2 raid-master=RAID6_array raid-role=1
/disk set disk3 raid-master=RAID6_array raid-role=2
/disk set disk4 raid-master=RAID6_array raid-role=3
/disk set disk5 raid-master=RAID6_array raid-role=4
/disk set disk6 raid-master=RAID6_array raid-role=5
/disk set disk7 raid-master=RAID6_array raid-role=6
/disk set disk8 raid-master=RAID6_array raid-role=7
/disk set RAID6_array nvme-tcp-export=yes
```

2.  Use the following commands on Client : 

3.  Your Client will now see a single disk, but it is actually a highly redundant RAID array. 

**==> picture [13 x 13] intentionally omitted <==**

In case you want to mount the block device on a Linux Client , then check the LinuxClient section. 

**==> picture [13 x 13] intentionally omitted <==**

Do not mount multiple disks from different RouterOS devices on a Linux Client and put them into a software RAID configuration (for example, mdadm). While this type of configuration does provide some redundancy, you can expect abnormal latency issues or even timeouts. It is recommended to create RAID array on your RouterOS and export the RAID array as a block device to your Linux Client.
