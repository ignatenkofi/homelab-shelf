## pull image: 

```
/container/add remote-image=pihole/pihole interface=veth1 root-dir=disk1/images/pihole
mounts=MOUNT_PIHOLE_PIHOLE,MOUNT_PIHOLE_DNSMASQD envlist=ENV_PIHOLE name=pihole
```

The image will be automatically pulled and extracted to root-dir, status can be checked by using 

1849 

```
/container/print
```
