## Web-Proxy cache configuration example 

Enter proxy cache path under IP -> Proxy menu and web proxy store is automatically created in files menu. If a non-existent directory path is used, an additional sub-directory is also created automatically. 

```
[admin@MikroTik] >  /ip proxy set cache-path=usb1/cache-n-db/proxy/
```

```
...
```

```
[admin@MikroTik] >  /file print
 # NAME                                              TYPE                             SIZE CREATION-TIME
 0 skins                                             directory                             mar/02/2015 18:56:23
 1 sys-note.txt                                      .txt file                        23   jul/03/2015 11:40:48
 2 usb1                                             disk                                  jul/03/2015 11:35:05
 3 usb1/lost+found                                  directory                             jul/03/2015 11:34:56
 4 usb1/cache-n-db                                  directory                             jul/03/2015 11:41:54
 4 usb1/cache-n-db/proxy                            web-proxy store                       jul/03/2015 11:42:09
```
