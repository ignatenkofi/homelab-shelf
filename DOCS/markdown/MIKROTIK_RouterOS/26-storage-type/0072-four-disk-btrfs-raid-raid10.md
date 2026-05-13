## Four disk Btrfs-RAID (RAID10) 

In case you want to create redundant and high capacity RAID10 array using Btrfs, follow the commands below. 

1.  Find the names of the disks you want to use for setting up a Btrfs-RAID: 

```
/disk print
```

**==> picture [13 x 13] intentionally omitted <==**

In this example, the disks used are going to be called `<disk-name-1>, <disk-name-2>, <disk-name-3> and <disk-name4>` , make sure you replace these placeholders with your actual disk names! 

2.  Format one of your disks to Btrfs, in this case `<disk-name-1>` : 

```
/disk format <disk-name-1> file-system=btrfs
```

3.  You can check the current status of Btrfs disks using the following command: 

```
/disk/btrfs/filesystem print
```

**==> picture [13 x 13] intentionally omitted <==**

In case there was an existing RAID on your disks and you want to remove any obsolete configuration for simplicity, then you can wipe the disks with `/disk format <disk-name-x> file-system=wipe-quick` . This is useful when you have unwanted entries under `/disk/btrfs/filesystem print` 

4.  Add a label for the Btrfs drive for simplicity: 

```
/disk/btrfs/filesystem set [find where present-devs=<disk-name-1>] label=BtrfsRAID
```
