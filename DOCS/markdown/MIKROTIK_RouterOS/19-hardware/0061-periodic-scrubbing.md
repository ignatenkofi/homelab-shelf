## Periodic scrubbing 

In a RAID array, you data is stored on multiple disks or multiple disks contain information how to reassemble the data. Without RAID your disks in rare events might corrupt a few bytes of your data and you might not even notice that the data has been corrupted. With RAID arrays your data is compared with other copies of data (or checked on assembly) when you read a file and will alert you that data is corrupted. With regular RAID and, for example, in RAID1 configuration the RAID array is not able to tell which copy of the file is correct, it will only inform you that the data corruption has been detected. With Btrfs RAID you are not only able to detect the data corruption, but you are also able to distinguish which copy of the file is the correct one by using checksums and restore it automatically. 

Scrubbing is a process that re-reads the whole RAID array and, in case of Btrfs RAID, corrects any data corruption. While Btrfs RAID will correct the data on file read operations, for example, you want to download a file from your RouterOS device, avoiding scrubbing is highly NOT recommended. In rare events it is possible that, for example, in RAID1 configuration both disks have corrupted data and Btrfs RAID might not be to restore the data. To avoid such situations and protect valuable data, consider running scrubbing on a regular basis. 

**==> picture [13 x 13] intentionally omitted <==**

Excessive detected data corruption usually indicated a failing storage device. Consider checking the storage device when you notice many data corruption warnings. 

The interval of how often to run scrubbing is going to depend on each use case. Scrubbing is an intensive task on your storage devices, it re-reads the whole RAID array and performs additional checks. During scrubbing you can experience noticeable performance drop since the disks until the scrubbing has finished. If you are worried about the performance during scrubbing, consider running scrubbing less often. If you are more worried about data integrity, consider running scrubbing more often. 

Summary: Used to detect and correct data corruption Recommended interval: 1 week 

Working example 

1695 

Example command: 

```
/disk/btrfs/filesystem/print
```

```
/disk/btrfs/filesystem/scrub-start 0
```

You can also cancel scrubbing using the following command: 

```
/disk/btrfs/filesystem/scrub-cancel
```
