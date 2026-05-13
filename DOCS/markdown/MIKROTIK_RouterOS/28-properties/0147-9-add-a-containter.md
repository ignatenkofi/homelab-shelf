## 9.  Add a Containter: 

```
/container/add remote-image=pihole/pihole interface=veth1 root-dir=disk1/images/pihole
mounts=MOUNT_PIHOLE_PIHOLE,MOUNT_PIHOLE_DNSMASQD envlist=ENV_PIHOLE name=pihole
```

**==> picture [13 x 13] intentionally omitted <==**

If You wish to see container output in `/log print` , then add `logging=yes` when creating a Container, root-dir should point to an external drive. It's not recommended to use internal storage for Containers. 

**==> picture [13 x 13] intentionally omitted <==**

There are multiple ways you can get a Container image, check the Adding a Container image section if you need an alternative way of adding a Container image. 

**==> picture [13 x 13] intentionally omitted <==**

Adding a Containter will start downloading or extracting it, the Container itself will not be started after it has been added, you need to start it manually for the first time after it has been downloaded/extracted. 

10.  Check the status of your Container and wait until downloading/extracting has been finished and the 

`status=stopped` : 

```
/container/print
```
