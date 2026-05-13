## Replacing a disk in Btrfs RAID array 

In case of a disk failure or you require to replace a disk in your existing Btrfs RAID array, then follow the procedure below: 

1.  Make sure you determine the correct disk that needs replacing. Use `/disk print detail` and `/disk/blink` to determine the correct disk. We will assume that the faulty disk is `disk2` . 

2.  Eject the faulty disk: 

```
/disk/eject disk2
```

3.  Physically remove the faulty disk 

4.  Print out the current status of your Btrfs RAID array: 

```
/disk/btrfs/filesystem/print
```

5.  Look for the `DEV-ID` in the commands output for the missing disk: 

1693 

```
[admin@MikroTik] /disk> /disk/btrfs/filesystem/print
Flags: I - MISSING-DEVS
Columns: LABEL, DEV-IDS, DEVS, DEFAULT-SUBVOLUME, SPACES, BALANCE-STATUS, UUID, WRITE-ERRORS, READ-
ERRORS, FLUSH-ERRORS, CORRUPTION-ERRORS, GENERATION-ERRORS
#   LABEL      DEV-IDS  DEVS     DEFAULT-SUBVOLUME  SPACES                                     BALANCE-
STATUS  UUID                                  W  R  F  C  G
0 I BtrfsRAID        1  disk1    <FS_ROOT>          disk1:480GB, used:0%
done            9246dfaa-be9f-4e08-a560-53cb8e82023b  0  0  0  0  0
                     2  missing                     data,raid1:1.07GB disk1:1.07GB, used:
0%                                                          0  0  0  0  0
                                                    data,single:1.07GB, used:
0%
                                                    system,raid1:33.6MB disk1:33.6MB, used:
0%
                                                    meta,raid1:1.07GB disk1:1.07GB, used:
0%
                                                    global-reserve:3.41MB, used:
0%
```

**==> picture [13 x 13] intentionally omitted <==**

In this case the missing disk's `DEV-ID` is "2". 

6.  Insert a new disk 7.  Determine the new disks name: 

```
/disk/print
```

**==> picture [13 x 13] intentionally omitted <==**

In this case the new disk's name is `disk3` 

8.  Run the following command to replace the disk in the Btrfs RAID array: 

```
/disk btrfs filesystem replace-device device-to-remove-id=2 device-to-add=disk3 BtrfsRAID
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure you set the correct `device-to-remove-id` to the `DEV-ID` that you determined previously! 

9.  Check the replace status and make sure that `REPLACE-STATUS` is marked as `done` . 

1694 

```
> /disk btrfs filesystem/print
Columns: LABEL, DEV-IDS, DEVS, DEFAULT-SUBVOLUME, SPACES, BALANCE-STATUS, REPLACE-STATUS, UUID, WRITE-
ERRORS, READ-ERRORS, FLUSH-ERRORS, CORRUPTION-ERRORS, GENERATION-ERRORS
# LABEL   DEV-IDS  DEVS   DEFAULT-SUBVOLUME  SPACES
BALANCE-STATUS  REPLACE-STATUS  UUID                                  WRITE-ERRORS  READ-ERRORS  F  C  G
0 BtrfsRAID     1  disk1  <FS_ROOT>          disk1:480GB, used:9%
done            done            9246dfaa-be9f-4e08-a560-53cb8e82023b             0            0  0  0  0
                2  disk3                     disk3:480GB, used:
9%
0            0  0  0  0
                                             data,raid1:40.8GB disk1:40.8GB disk3:40.8GB, used:
72%
                                             system,raid1:101MB disk1:101MB disk3:101MB, used:
0%
                                             meta,raid1:3.22GB disk1:3.22GB disk3:3.22GB, used:
1%
                                             global-reserve:30.7MB, used:
0%
```

**==> picture [13 x 13] intentionally omitted <==**

Ensure that your Btrfs RAID array does not have inconsistent Btrfs profiles for `data` , `system` or `meta` . The desired profiles will depend on your specific setup. For RAID1 setups you will most likely want these profiles to match, but in RAID10 setup these values can be different. In any RAID setup there should not be a `single` profile for either `data` , `system` nor `meta` .
