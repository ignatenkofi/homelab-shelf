## Tips and tricks 

Containers use up a lot of disk space, USB/SATA, NVMe attached media is highly recommended. For devices with USB ports - USB to SATA adapters can be used with 2.5" drives - for extra storage and faster file operations. 

RAM usage can be limited by using: 

```
/container/config/set memory-high=200M
```

this will soft limit RAM usage - if a RAM usage goes over the high boundary, the processes of the cgroup are throttled and put under heavy reclaim pressure. 

For starting containers after router reboot use start-on-boot option (starting from 7.6beta6) 

```
/container/print
```

```
 0 name="2e679415-2edd-4300-8fab-a779ec267058" tag="test_arm64:latest" os="linux" arch="arm"
interface=veth2
   root-dir=disk1/alpine mounts="" dns="" logging=yes start-on-boot=yes status=running
```

```
/container/set 0 start-on-boot=yes
```

It is possible to get to running container shell: 

```
/container/shell 0
```

Enable logging to get output from container: 

```
/container/set 0 logging=yes
```

1854 

Some containers will require additional privileges in order to be able to run properly: 

```
/container/set 0 user=0:0
```

You can execute commands inside a Container with a specific user and without invoking /bin/sh: 

```
/container shell nextcloud user=www-data cmd="php /var/www/html/cron.php" no-sh
```

Starting from 7.11beta5 version multiple addresses and ipv6 addresses can be added: 

```
interface/veth add address=172.17.0.3/16,fd8d:5ad2:24:2::2/64 gateway=172.17.0.1 gateway6=fd8d:5ad2:24:
2::1
```

Active running /dev/ nodes to container: 

```
/dev/full        /dev/null        /dev/random                /dev/tty        /dev/urandom        /dev
/zero        /dev/console        /dev/net/tun        /dev/kvm        /dev/fuse
```

1855
