## Overview 

File menu shows all user space files on the router. It is possible to create a new file, directory, edit file content, delete file or directory.  If RouterOS ".npk" package is uploaded, the file menu will also show package-specific information, for example, architecture, build date and time, etc. 

**==> picture [13 x 13] intentionally omitted <==**

It is possible to retrieve content and edit files up to 60KB in size. For accessing contents of larger files, please refer to section Get File Contents. 

```
[admin@MikroTik] > file print detail
```

```
 0 name=wireless-7.16.1-arm.npk type=package size=1924.1KiB last-modified=2024-11-25 13:14:28 package-name="
wireless" package-version="7.16.1" package-build-time=2024-10-10 14:03:32
   package-architecture="arm"
```

```
 1 name=routeros-7.16.1-arm.npk type=package size=11.1MiB last-modified=2024-11-25 13:14:34 package-name="
system" package-version="7.16.1" package-build-time=2024-10-10 14:03:32
   package-architecture="arm"
```

```
 2 name=flash type=disk last-modified=2024-11-25 13:12:10
```

```
 3 name=flash/skins type=directory last-modified=2024-11-25 13:10:52
```

```
 4 name=flash/skins/newskin.json type=.json file size=0 last-modified=2024-11-25 13:10:52
```

```
 5 name=flash/filename type=file size=0 last-modified=2024-11-25 13:11:58
```

```
 6 name=flash/directory_name type=directory last-modified=2024-11-25 13:12:10
```
