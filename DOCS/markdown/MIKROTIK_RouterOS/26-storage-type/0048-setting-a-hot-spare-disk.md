## Setting a hot spare disk 

It's possible to assign a hot spare disk for your RAID array. In case of a disk failure - the rebuild immediately begins on the assigned spare disk. 

Add the RAID array with the desired amount of arrays: 

```
/disk add raid-device-count=4 raid-type=5 type=raid slot=raid5
```

Afterwards, add the disks to the RAID as well as the spare. In this case we will add NVMe5 as the spare. 

```
/disk set raid-master=raid5 raid-role=0 nvme1
/disk set raid-master=raid5 raid-role=1 nvme2
/disk set raid-master=raid5 raid-role=2 nvme3
/disk set raid-master=raid5 raid-role=3 nvme4
/disk set raid-master=raid5 raid-role=spare nvme5
```
