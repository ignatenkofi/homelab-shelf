## Formatting attached storage unit - Simple 

1. Disk is attached, and already mounted automatically by the system. 

1662 

```
[admin@MikroTik] > disk print
Flags: B - BLOCK-DEVICE; M, F - FORMATTING
Columns: SLOT, MODEL, SERIAL, INTERFACE, SIZE, FREE, FS
#    SLOT  MODEL           SERIAL            INTERFACE                  SIZE           FREE  FS
0 BM usb1  USB Flash Disk  FBA0911260071572  USB 2.00 480Mbps  2 004 877 312  1 921 835 008  ext4
```

```
[admin@MikroTik] > /file print
 # NAME                        TYPE          SIZE CREATION-TIME
 0 skins                       directory          jan/01/1970 03:00:01
 1 pub                         directory          feb/04/1970 21:31:40
 2 usb1                        disk               mar/07/2022 14:05:16
```

2. Formatting the disk, in either of two supported file-systems (ext4 or fat32). 

```
[admin@MikroTik] > /disk format usb1 file-system=ext4 mbr-partition-table=no
  formatted: 100%
```

3. It's done! Drive is formatted and should be automatically mounted after formatting process is finished.
