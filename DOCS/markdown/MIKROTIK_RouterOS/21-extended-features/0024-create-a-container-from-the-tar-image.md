## Create a container from the tar image 

```
/container/add file=pihole.tar interface=veth1 mounts=MOUNT_PIHOLE_PIHOLE,MOUNT_PIHOLE_DNSMASQD
envlist=ENV_PIHOLE name=pihole
```
