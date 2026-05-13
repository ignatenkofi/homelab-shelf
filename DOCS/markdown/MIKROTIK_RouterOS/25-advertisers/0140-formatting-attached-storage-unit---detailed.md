## Formatting attached storage unit - Detailed 

Let us presume that you have added a storage device to your device that is running RouterOS. System will try to automatically mount it and in such case if storage is formatted in a supported file-system and partition record, it will be found in "/files" menu moments after you plugged it in to the host device. 

If not, here is what you have to do. 

1. Do a quick print of disk menu, to make sure that router sees the attached storage. 

```
[admin@MikroTik] > disk print
Flags: B - BLOCK-DEVICE; M, F - FORMATTING
Columns: SLOT, MODEL, SERIAL, INTERFACE, SIZE, FREE, FS
#    SLOT  MODEL           SERIAL            INTERFACE                  SIZE           FREE  FS
0 BM usb1  USB Flash Disk  FBA0911260071572  USB 2.00 480Mbps  2 004 877 312  1 921 835 008  ext4
```

We can here see that system sees one storage drive and also that it is formatted with a known file-system type. 

When running file menu print-out we also see that is mounted. 

```
[admin@MikroTik] > file print
 # NAME     TYPE    SIZE CREATION-TIME
 0 usb1     disk         mar/07/2022 14:05:16
 1 skins    directory    jan/01/1970 03:00:01
 2 pub      directory    feb/04/1970 21:31:40
```

2. To formatting drive - we issue command with previously know id or name(slot) and with desired file-system (ext4 or fat32), we can also assign label to device as I did in this example and make mbr partition table 

```
[admin@MikroTik] > /disk format usb1 file-system=ext4 label=usb-flash mbr-partition-table=yes
  formatted: 100%
```

**==> picture [13 x 13] intentionally omitted <==**

Note: In printout, you can see that there is a progress percentage counter in formatting process. For larger storage drives, it might take longer for this process to finish, so be patient. 

Creating multiple disk partitions 

1663 

If multiple GPT partitions are needed format drive without partition table and add them manually: 

```
[admin@MikroTik] > /disk format usb1 file-system=ext4 label=usb-flash mbr-partition-table=no
  formatted: 100%
```

```
[admin@MikroTik] > /disk add type=partition parent=usb1 partition-size=200M
[admin@MikroTik] > /disk add type=partition parent=usb1 partition-size=500M
[admin@MikroTik] > /disk add type=partition parent=usb1 slot=usb1-last-partition
```

**==> picture [13 x 13] intentionally omitted <==**

Note: Slot (partition or disk name) is assumed automatically, but can be overwritten by using slot parameter. If partition size is not used all available space will be used from last partition. To offset partition start "partition-offset" parameter can be used.
