## Getting image 

To simplify the configuration, we will get the image from an external library but you can also import it via the .tar file. 

In this example, we will use the device's own storage. RB1100AHx4 has 128 MB disk space and a basic mosquitto installation should not take up more than ~15 MB. 

Make sure that you have "Registry URL" set accordingly, limit RAM usage (if necessary), and set up a directory for the image: 

- `/container/config/set registry-url=https://registry-1.docker.io tmpdir=pull`
