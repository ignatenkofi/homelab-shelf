## Swap partition 

Swap partition requires you to have a disk (or partition) connected to your RouterOS device. All the disk (or partition) will be used as swap space and cannot be used for other purposes. Make sure you a high speed disk for your swap partition. Using a swap partition has a better performance than using a swap file.   | 

To use a disk (or partition) as a swap partition, you can use the following command: 

```
/disk set disk1 swap=yes
```

Make sure you change `disk1` to your correct disk's name! 

1665
