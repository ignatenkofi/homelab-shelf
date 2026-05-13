## Configuration example 

Basic configuration is really easy, on the host device you need to add the file you want to sync to another device, the ip, user/password and the mode. 

```
/file sync
```

```
add local-path=/ipv6route.txt.rsc mode=upload remote-address=192.168.88.2 remote-path=RAID/
```

If configured correctly, you will see on the host device: 

```
0 192.168.88.2  upload  /ipv6route.txt.rsc  RAID/        in sync
```
