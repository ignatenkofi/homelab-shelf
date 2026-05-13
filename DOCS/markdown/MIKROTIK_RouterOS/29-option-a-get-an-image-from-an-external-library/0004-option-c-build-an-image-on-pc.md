## Option C: Build an image on PC 

You can build your own Containers and use them on your RouterOS device. While you can build Containers using Docker, we recommend using Podman since it is easier to build Containers for a specific architecture using Podman. 

1.  Get source files for your required Container image, for example by using git: 

```
git clone https://github.com/pi-hole/docker-pi-hole.git
cd docker-pi-hole
```

2.  Build the Container image by specifying the Dockerfile or Containerfile and the target archiceture: 

```
#For ARM64
podman build --platform linux/arm64 --tag pihole -f ./src/Dockerfile
```

```
#For ARM
podman build --platform linux/arm --tag pihole -f ./src/Dockerfile
```

```
#For AMD64
podman build --platform linux/amd64 --tag pihole -f ./src/Dockerfile
```

3.  Save the container image to an archive: 

1850 

```
podman save pihole > pihole.tar
```
