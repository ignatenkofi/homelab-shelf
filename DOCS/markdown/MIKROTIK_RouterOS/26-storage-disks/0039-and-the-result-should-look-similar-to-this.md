## And the result should look similar to this 

```
21 BM        type=raid slot="raid1" slot-default="" parent=none uuid="f457bc79-7408-489b-8850-85923e900452"
fs=ext4 model="RAID6 2-parity-disks"
```

```
             size=17 283 541 893 120 free=17 283 538 190 336 raid-type=6 raid-device-count=20 raid-max-
component-size=none raid-chunk-size=1M raid-master=none
```

```
             raid-state="clean" nvme-tcp-export=no iscsi-export=no nfs-sharing=no smb-sharing=no media-
sharing=no media-interface=none
```

1674 

**==> picture [13 x 13] intentionally omitted <==**

Avoid using multiple partitions on a single physical disk in multiple RAID arrays. Using the the same physical disk in multiple RAID arrays can result in low performance.
