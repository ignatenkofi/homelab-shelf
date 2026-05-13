## 4.  Upload the archive to your RouterOS device, for example: 

```
rsync -av pihole.tar admin@192.168.88.1:/data/disk1/
```

**==> picture [13 x 13] intentionally omitted <==**

You can also use Winbox to upload files! 

5.  Create a Container on your RouterOS device using the uploaded container image archive file: 

```
/container/add file=disk1/pihole.tar interface=veth1 root-dir=disk1/pihole mounts=MOUNT_PIHOLE_PIHOLE,
MOUNT_PIHOLE_DNSMASQD envlist=ENV_PIHOLE name=pihole
```
