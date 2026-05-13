## Using FTP 

Open your favorite SFTP program (in this case it is Filezilla), select the package, and upload it to your router (demo2.mt.lv is the address of my router in this example). note that in the image I'm uploading many packages, but in your case - you will have one file that contains them all if you wish, you can check if the file is successfully transferred onto the router (optional): 

```
[admin@MikroTik] >/file print
Columns: NAME, TYPE, SIZE, CREATION-TIME
#  NAME                  TYPE       SIZE     CREATION-TIME
0  routeros-7.9-arm.npk  package    13.0MiB  may/18/2023 16:16:18
1  pub                   directory           nov/04/2022 11:22:19
2  ramdisk               directory           jan/01/1970 03:00:24
```

reboot your router for the upgrade process to begin: 

```
[admin@MikroTik] >/system reboot
Reboot, yes? [y/N]: y
```

after the reboot, your router will be up to date, you can check it in this menu: 

- `[admin@MikroTik] >/system package print` 

if your router did not upgrade correctly, make sure you check the log 

```
[admin@MikroTik] >/log print without-paging
```
