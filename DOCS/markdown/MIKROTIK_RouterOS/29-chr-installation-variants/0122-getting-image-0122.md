## Getting image 

To simplify the configuration, we will get the image from an external library but you can also import it via the .tar file. 

Make sure that you have "Registry URL" set accordingly, limit RAM usage (if necessary), and set up a directory for the image. 

```
/container/config/set registry-url=https://registry-1.docker.io tmpdir=pull ram-high=2048.0MiB
```

Pull image: `/container/add remote-image=thingsboard/tb-postgres:latest interface=veth1 root-dir=ThingsBoard mounts=mytbdata,mytb-logs envlist=tb_envs logging=yes` 

After running the command, RouterOS should start "extracting" the package. Check "File System" for newly created folders and monitor container status with the command `/container/print` .
