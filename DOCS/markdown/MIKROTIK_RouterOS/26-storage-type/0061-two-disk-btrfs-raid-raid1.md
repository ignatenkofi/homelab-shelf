## Two disk Btrfs-RAID (RAID1) 

In case you want to create a reliable data storage solution with just two disks (for example, NAS), then you can follow this these steps to successfully create a RAID1 array with Btrfs: 

1.  Find the names of the disks you want to use for setting up a Btrfs-RAID: 

```
/disk print
```

**==> picture [13 x 13] intentionally omitted <==**

In this example, the disks used are going to be called `<disk-name-1>` and `<disk-name-2>` , make sure you replace these placeholders with your actual disk names! 

2.  Format one of your disks to Btrfs, in this case `<disk-name-1>` : `/disk format <disk-name-1> file-system=btrfs` 

3.  You can check the current status of Btrfs disks using the following command: 

1683 

```
/disk/btrfs/filesystem print
```

**==> picture [13 x 13] intentionally omitted <==**

In case there was an existing RAID on your disks and you want to remove any obsolete configuration for simplicity, then you can wipe the disks with `/disk format <disk-name-x> file-system=wipe-quick` . This is useful when you have unwanted entries under `/disk/btrfs/filesystem print`
