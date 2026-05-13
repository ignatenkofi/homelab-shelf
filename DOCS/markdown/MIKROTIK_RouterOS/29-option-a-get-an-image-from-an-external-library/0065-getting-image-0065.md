## Getting image 

To simplify the configuration, we will get the images from an external library. 

Make sure that you have "Registry URL" set accordingly, limit RAM usage (if necessary), and set up a directory for the images: 

```
/container/config/set registry-url=https://registry-1.docker.io tmpdir=/usb1/pull
```

Pull home-assistant image and wait for it to be extracted: 

```
/container/add remote-image=homeassistant/home-assistant:latest interface=veth2 root-dir=/usb1/ha
mounts=ha_config envlist=ha_env logging=yes
```

After running the command, RouterOS should start "extracting" the package. Check "File System" for newly created folders and monitor container status with the command `/container/print` .
