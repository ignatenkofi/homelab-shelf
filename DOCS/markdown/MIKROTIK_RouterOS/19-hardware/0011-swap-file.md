## Swap file 

Swap file requires you to have a disk that is formatted with a file system, for example, Btrfs. Compared to the swap partition option, the whole disk (or partition) will not be used as swap space, only the swap file's size will be used on your disk (or partition). Using a swap file will have a lower performance than using a swap partition. 

To create a swap file on your existing file system , you can use the following command: 

```
/disk add type=file file-path=disk1/swapfile file-size=1G swap=yes
```

Make sure you change `disk1` to your correct path, where your disk is mounted.
