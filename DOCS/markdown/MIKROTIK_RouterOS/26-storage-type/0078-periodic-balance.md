## Periodic balance 

In Btrfs data is stored in allocated chunks, which then allows storing your data in blocks. Over time due to various data activities, the chunks can become partially full and distributed between many chunks in a sub optimal way. Balancing a Btrfs file system means re-arranging the data in these chunks and restoring the unallocated space. As a result you can restore lost usable free space and performance of the Btrfs file system. This is somewhat similar to a defragmentation operation on other file systems. 

An important parameter for balancing is the `data-usage` parameter. This is a filter that prevents the balancing function to process chunks that are above a certain usage percentage. For example, `data-usage=50` will only process chunks that are 50% full or less. You can run the balancing command multiple times with different values and therefore reduce the amount of time each balancing operation requires. Balancing can be an intensive task depending on your free space available and how data has been written since last balancing action therefore you might benefit of running the balance command with different `data-usage` values on separately to reduce the time window when balancing causes a performance drop due to intensive disk reads and writes. 

In case you want to run balancing commands separately, you should use `data-usage` values of 25, 50, 75 and 90. It is not recommended to go above 90%. For most users running balance command separately is not required and running it once per interval with `data-usage` of 50% is sufficient. 

Summary: Used to restore free space and improve performance Recommended interval: twice a month 

Recommended `data-usage` : 50 Working example 

Example command: 

```
/disk/btrfs/filesystem/print
```

```
/disk/btrfs/filesystem/balance-start data-usage=50 0
```

You can also cancel balance using the following command: 

```
/disk/btrfs/filesystem/balance-cancel
```
