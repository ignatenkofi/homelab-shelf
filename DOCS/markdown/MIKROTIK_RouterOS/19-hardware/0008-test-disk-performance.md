## Test disk performance 

**==> picture [13 x 13] intentionally omitted <==**

Disk performance tests may slowly degrade disk health On write tests all files and file systems on disks will be destroyed 

Starting from 7.16 to run disk performance tests. Disks has to be disabled or without mountable file system (unformatted). Check available disks, if disk is already mounted - disable it. 

```
[admin@MikroTik] > disk print
Flags: B - BLOCK-DEVICE; M - MOUNTED
Columns: SLOT, MODEL, SERIAL, INTERFACE, SIZE, FREE, FS
#    SLOT  MODEL             SERIAL         INTERFACE                    SIZE            FREE  FS
0 BM usb1  JMicron External  DD56419883891  USB 3.10 5000Mbps  64 023 257 088  62 692 188 160  ext4
[admin@MikroTik] > disk disable usb1
```

```
[admin@MikroTik] > disk test disk=usb2 pattern=sequential  type=device thread-count=4 block-size=4K
direction=write
Columns: SEQ, RATE, IOPS, DISK, TYPE, PATTERN, DIR, BSIZE, THREADS
SEQ  RATE          IOPS  DISK  TYPE    PATTERN     DIR    BSIZE  THREADS
0    1622.5Mbps  49 516  usb2  device  sequential  write   4096        4
1    26.2Mbps       800  usb2  device  sequential  write   4096        4
2    33.0Mbps     1 008  usb2  device  sequential  write   4096        4
3    11.7Mbps       360  usb2  device  sequential  write   4096        4
4    28.5Mbps       872  usb2  device  sequential  write   4096        4
5    34.6Mbps     1 056  usb2  device  sequential  write   4096        4
6    33.8Mbps     1 032  usb2  device  sequential  write   4096        4
TOT  255.7Mbps    7 806  usb2  device  sequential  write   4096        4
```
