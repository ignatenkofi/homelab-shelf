## 6.  Start Btrfs balance process to create a Btrfs-RAID with RAID1 configuration: 

```
/disk/btrfs/filesystem balance-start [find where label=BtrfsRAID] data-profile=raid10 metadata-
profile=raid1c4 system-profile=raid1c4
```

1692 

**==> picture [13 x 13] intentionally omitted <==**

There are many possible configurations of `data-profile` , `metadata-profile` and `system-profile` . For a RAID10 array it is recommended to use either `raid1c3` or `raid1c4` for both `system-profile` and `metadata-profile. The raid1c4 profile is going to store 4 copies of the data on different disks, this makes the data more redundant, but uses more disk space.` 

**==> picture [13 x 13] intentionally omitted <==**

Btrfs RAID5 and RAID6 is not supported. Use regular RAID if you need such RAID configurations. Be aware that when using regular RAID with Btrfs you will not have bit-rot protection. 

**==> picture [13 x 13] intentionally omitted <==**

For most use cases set `metadata-profile` to the same value as `system-profile` . Avoid using different values for both of these profiles. 

7.  Set `mount-filesystem=no` for other disks to prevent the files showing up twice: 

```
/disk set <disk-name-2> mount-filesystem=no
/disk set <disk-name-3> mount-filesystem=no
/disk set <disk-name-4> mount-filesystem=no
```

8.  You can also change the mount point's name for simplicity: 

```
/disk set <disk-name-1> mount-point-template=BtrfsRAID
```

9.  Your newly created Btrfs-RAID array is now accessible through `/BtrsRAID/` folder.
