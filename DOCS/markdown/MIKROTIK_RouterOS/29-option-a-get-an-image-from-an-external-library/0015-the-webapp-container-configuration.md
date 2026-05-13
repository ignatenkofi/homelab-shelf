## The webapp Container configuration: 

```
/container/add remote-image=dpage/pgadmin4 interface=veth1 root-dir=disk1/images/pgadmin name=pgadmin
start-on-boot=yes logging=yes
```

In this example, the `pgadmin` port 80 is accessible to everyone, but the `postgres` port 5432 is not accessible to everyone, it can only be accessed through either `pgadmin` as `127.0.0.1` or through the RouterOS device running the Containter as `172.17.0.2` .
