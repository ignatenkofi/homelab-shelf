## Configuration example 

In this example I'm using 10 SSD drives and configuring in RAID (RAID 1+0) 

Create a RAID 0 block 

```
add raid-device-count=3 raid-type=0 slot=raid10 type=raid
```

Create five RAID 1 blocks, each containing 2 devices and add them to set the master-raid the previously created RAID 0 block (name=raid10) 

```
add raid-device-count=2 raid-master=raid10 raid-role=0 raid-type=1 slot=raid0 type=raid
add raid-device-count=2 raid-master=raid10 raid-role=1 raid-type=1 slot=raid1 type=raid
add raid-device-count=2 raid-master=raid10 raid-role=2 raid-type=1 slot=raid2 type=raid
add raid-device-count=2 raid-master=raid10 raid-role=3 raid-type=1 slot=raid3 type=raid
add raid-device-count=2 raid-master=raid10 raid-role=4 raid-type=1 slot=raid4 type=raid
```

1678 

Add drives to each RAID block 

```
set nvme1 raid-master=raid0 raid-role=0
set nvme3 raid-master=raid1 raid-role=0
set nvme5 raid-master=raid2 raid-role=0
set nvme7 raid-master=raid3 raid-role=0
set nvme9 raid-master=raid4 raid-role=0
```

```
set nvme2 raid-master=raid0 raid-role=1
set nvme4 raid-master=raid1 raid-role=1
set nvme6 raid-master=raid2 raid-role=1
set nvme8 raid-master=raid3 raid-role=1
set nvme10 raid-master=raid4 raid-role=1
```

After this format, the raid10 block 

```
format raid10 file-system=ext4
```

After formating you should see the free space and use the block 

```
23 BM        type=raid slot="raid10" slot-default="" parent=none uuid="ec3344f4-1662-49ab-b899-db1aaa217b0f"
fs=ext4 model="RAID0 striped" size=9 601 967 652 864
```

```
             free=9 597 901 369 344 raid-type=0 raid-device-count=5 raid-max-component-size=none raid-
master=none raid-state="clean" nvme-tcp-export=no
```

```
             iscsi-export=no nfs-sharing=no smb-sharing=no media-sharing=no media-interface=none
```

Based on this configuration you can modify the RAID 10 configuration to fit as much storage devices as you require. 

Similarly it is possible to create other nested RAID configurations, keeping the same principle as showcased in the example.
