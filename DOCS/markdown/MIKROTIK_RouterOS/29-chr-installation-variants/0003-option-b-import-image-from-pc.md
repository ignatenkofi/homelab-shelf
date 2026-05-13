## Option B: Import image from PC 

Your can use your PC running either Docker or Podman to download your required container image and save it to an archive. We recommend using Podm an since it is easier to build and download containers for specific architectures using Podman. 

1.  Download your required image based on the architecture of your RouterOS device: 

```
#For ARM64
podman pull --arch=arm64 docker.io/pihole/pihole
#For ARM
podman pull --arch=arm docker.io/pihole/pihole
#For AMD64
podman pull --arch=amd64 docker.io/pihole/pihole
```

2.  Save the container image to an archive: 

```
podman save pihole > pihole.tar
```

3.  Upload the archive to your RouterOS device, for example: 

```
rsync -av pihole.tar admin@192.168.88.1:/data/disk1/
```

**==> picture [13 x 13] intentionally omitted <==**

You can also use Winbox to upload files! 

4.  Create a Container on your RouterOS device using the uploaded container image archive file: 

```
/container/add file=disk1/pihole.tar interface=veth1 root-dir=disk1/pihole mounts=MOUNT_PIHOLE_PIHOLE,
MOUNT_PIHOLE_DNSMASQD envlist=ENV_PIHOLE name=pihole
```
