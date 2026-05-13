## Pull image: 

- `/container/add remote-image=library/eclipse-mosquitto:latest interface=veth2 root-dir=mosquitto mounts=msqt_config logging=yes` 

After running the command, RouterOS should start "extracting" the package. Check "File System" for newly created folders and monitor container status with the command `/container/print` .
