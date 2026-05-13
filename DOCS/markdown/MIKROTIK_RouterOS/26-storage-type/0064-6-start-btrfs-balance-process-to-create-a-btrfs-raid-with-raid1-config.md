## 6.  Start Btrfs balance process to create a Btrfs-RAID with RAID1 configuration: 

```
/disk/btrfs/filesystem balance-start [find where label=BtrfsRAID] data-profile=raid1 metadata-
profile=raid1 system-profile=raid1
```

7. IMPORTANT: Double check that all Btrfs profiles for the disks match, in this case you need to make sure that the `data` , `meta` and `system` profile is `raid1` 

```
/disk/btrfs/filesystem/print
```

**==> picture [13 x 13] intentionally omitted <==**

If you notice, for example, in the output `data,single:1` , then you will need to execute the `/disk/btfs/filesystem balancestart` command again. 

**==> picture [13 x 13] intentionally omitted <==**

The desired state is when the output is similar to the one below with Btrfs profile for `data` , `system` and `meta set to raid1` : 

```
> /disk/btrfs/filesystem/print
...
data,raid1:1.07GB disk1:1.07GB disk2:1.07GB, used:
0%
system,raid1:33.6MB disk1:33.6MB disk2:33.6MB, used:
0%
meta,raid1:1.07GB disk1:1.07GB disk2:1.07GB, used:0%
```

**==> picture [13 x 13] intentionally omitted <==**

Use the BtrfsRAIDCheck script to warn you about Btrfs profile inconsistencies! 

8.  Set `mount-filesystem=no` for second disk to prevent the files showing up twice: 

```
/disk set <disk-name-2> mount-filesystem=no
```

1684 

**==> picture [13 x 13] intentionally omitted <==**

Btrfs has feature that allows you to mount any of the Btrfs-RAID members and you will still be able to access the whole Btrfs-RAID array. A downside of this feature is that if you have mounted the same array twice, then your files will appear twice as well. To prevent this, you can simply disable mounting one of the Btrfs-RAID members automatically. 

9.  You can also change the mount point's name for simplicity: 

```
/disk set <disk-name-1> mount-point-template=BtrfsRAID
```

10.  Your newly created Btrfs-RAID array is now accessible through `/BtrsRAID/` folder. 

With a reliable storage solution such as Btrfs-RAID consider adding useful features to your RouterOS device by following the suggested guides below: 

running your own Containers DLNA Media Server Samba server NFS server 

**==> picture [13 x 13] intentionally omitted <==**

- When regular RAID is used with Btrfs filesystem, then your RAID array will not be able to heal itself from Bitrot, your RAID array can only detect Bitrot with regular RAID. It is recommended to use Btrfs-RAID (the configuration described in this section) when possible.
