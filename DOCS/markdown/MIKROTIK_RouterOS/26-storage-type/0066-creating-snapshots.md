## Creating snapshots 

Snapshots are space efficient way to create backups for your data. By creating a snapshot you save the current state of your data which you can later access. 

1688 

**==> picture [13 x 13] intentionally omitted <==**

Snapshots don't create a copy of your data, they save the current state of your data while allowing to make changes to your current data. Snapshots contain the information on how to revert the current data to a state that was present at the time when the snapshot was created. Snapshots don't create multiple copies of your data like, for example, a full backup does. 

**==> picture [13 x 13] intentionally omitted <==**

While you can create snapshots of a root subvolume, it is recommended to create a new subvolume for your data and then use the snapshot feature. This is only a preference when managing many snapshots. 

1.  Create subvolumes (or use the root subvolume, see above) and put data inside these subvolumes, for example: 

```
[admin@MikroTik] > /file print
 # NAME
 0 BtrfsDisk
 1 BtrfsDisk/Documents
 2 BtrfsDisk/Photos
 3 BtrfsDisk/Documents/document1.txt
 4 BtrfsDisk/Photos/photo1.jpg
```

2.  In this example, we have created `/Btrfs/Documents` and `/Btrfs/Photos/` subvolumes and you can view them with: 

```
/disk/btrfs/subvolume/print
```

3.  In order to make snapshots more organized, create a new subvolume called `Snapshots` : 

```
/disk/btrfs/subvolume/add name=Snapshots fs=BtrfsDisk
```

4.  Create a snapshot for `Documents` and `Photos` : 

```
/disk/btrfs/subvolume/add read-only=yes parent=Documents fs=BtrfsDisk  name=Snapshots/Documents-22012025
/disk/btrfs/subvolume/add read-only=yes parent=Photos fs=BtrfsDisk  name=Snapshots/Photos-22012025
```

5.  You should now have new subvolumes that are read-only and contain your files: 

```
[admin@MikroTik] > /file print
 # NAME
 0 BtrfsDisk
 1 BtrfsDisk/Documents
 2 BtrfsDisk/Photos
```

```
 3 BtrfsDisk/Snapshots
```

```
 4 BtrfsDisk/Documents/document1.txt
```

```
 5 BtrfsDisk/Photos/photo1.jpg
```

```
 6 BtrfsDisk/Snapshots/Documents-22012025
```

```
 7 BtrfsDisk/Snapshots/Photos-22012025
```

```
 8 BtrfsDisk/Snapshots/Documents-22012025/document1.txt
```

```
 9 BtrfsDisk/Snapshots/Photos-22012025/photo1.jpg
```

6.  For testing purposes, you can add more data to your subvolumes and you should notice that newly added files do not appear in the snapshots, but only in the subvolumes: 

1689 

```
[admin@infra1.mikrotikls.lv] > /file print
 # NAME
 0 BtrfsDisk
 1 BtrfsDisk/Documents
 2 BtrfsDisk/Photos
 3 BtrfsDisk/Snapshots
 4 BtrfsDisk/Documents/document1.txt
```

```
 5 BtrfsDisk/Documents/document2.txt
```

```
 6 BtrfsDisk/Photos/photo1.jpg
 7 BtrfsDisk/Photos/photo2.jpg
 8 BtrfsDisk/Snapshots/Photos-22012025
 9 BtrfsDisk/Snapshots/Documents-22012025
10 BtrfsDisk/Snapshots/Documents-22012025/document1.txt
11 BtrfsDisk/Snapshots/Photos-22012025/photo1.jpg
```

7.  You can now create a new snapshot: 

```
/disk/btrfs/subvolume/add read-only=yes parent=Documents fs=BtrfsDisk  name=Snapshots/Documents-23012025
/disk/btrfs/subvolume/add read-only=yes parent=Photos fs=BtrfsDisk  name=Snapshots/Photos-23012025
```

8.  After a new snapshot, you will have 2 snapshots for each subvolume. One contains older files and another one contains older and newer files: 

```
[admin@MikroTik] > /file print
 # NAME
 0 BtrfsDisk
 1 BtrfsDisk/Documents
 2 BtrfsDisk/Photos
 3 BtrfsDisk/Snapshots
 4 BtrfsDisk/Documents/document1.txt
 5 BtrfsDisk/Documents/document2.txt
 6 BtrfsDisk/Photos/photo1.jpg
 7 BtrfsDisk/Photos/photo2.jpg
 8 BtrfsDisk/Snapshots/Photos-22012025
 9 BtrfsDisk/Snapshots/Documents-22012025
10 BtrfsDisk/Snapshots/Documents-23012025
11 BtrfsDisk/Snapshots/Photos-23012025
12 BtrfsDisk/Snapshots/Documents-22012025/document1.txt
13 BtrfsDisk/Snapshots/Documents-23012025/document1.txt
14 BtrfsDisk/Snapshots/Documents-23012025/document2.txt
15 BtrfsDisk/Snapshots/Photos-22012025/photo1.jpg
16 BtrfsDisk/Snapshots/Photos-23012025/photo1.jpg
17 BtrfsDisk/Snapshots/Photos-23012025/photo2.jpg
```

**==> picture [13 x 13] intentionally omitted <==**

Multiple snapshots do not create multiple copies of each file, but if a file has been deleted and it still exists in a snapshot, then the deleted file will take up space. If a file exists in multiple snapshots, then it will take up space for only 1 file. 

9.  In case you don't need an older snapshot, you can delete it: 

```
/disk/btrfs/subvolume/remove [find where name=Documents-22012025]
/disk/btrfs/subvolume/remove [find where name=Photos-22012025]
```
