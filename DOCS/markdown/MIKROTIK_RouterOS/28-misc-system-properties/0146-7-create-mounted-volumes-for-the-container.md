## 7.  Create mounted volumes for the Container: 

```
/container/mounts/add name=MOUNT_PIHOLE_PIHOLE src=disk1/volumes/pihole/pihole dst=/etc/pihole
/container/mounts/add name=MOUNT_PIHOLE_DNSMASQD src=disk1/volumes/pihole/dnsmasq.d dst=/etc/dnsmasq.d
```

**==> picture [13 x 13] intentionally omitted <==**

`src=` points to RouterOS location (could also be `src=disk1/etc_pihole` if, for example, You decide to put configuration files on external USB media), `dst=` points to defined location (consult containers manual/wiki/github for information on where to point). If `src` d irectory does not exist on first time use then it will be populated with whatever container have in `dst` location. 

**==> picture [13 x 13] intentionally omitted <==**

It is highly recommended to place any Container volume on an attached disk to your RouterOS device. Avoid placing Container volumes on the built-in storage. 

8.  Configure to use a specific Container repository, for example, to use Docker.io: 

1848 

```
/container/config/set registry-url=https://registry-1.docker.io tmpdir=disk1/tmp
```
