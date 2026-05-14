## Container in Layer2 network 

In this networking setup, your Container is directly attached to a Layer2 network with other physical network devices. This networking setup is equivalent to "host" networking mode on other Container engines such as Docker. 

**==> picture [13 x 13] intentionally omitted <==**

In this networking setup, all the ports on your Container are exposed. This is considered insecure, but does slightly improve the Container's networking performance. 

The networking configuration: 

```
/interface/veth/add name=veth1 address=192.168.88.2/24 gateway=192.168.88.1
```

```
/interface/bridge/port add bridge=bridge interface=veth1
```

In case your RouterOS device has services running on the same port, you need to disable them: 

```
/ip service/disable [find where name=www]
```

The webapp configuration: 

```
/container/add remote-image=dpage/pgadmin4 interface=veth1 root-dir=disk1/images/pgadmin name=pgadmin
start-on-boot=yes logging=yes
```

1853 

In this example, `pgadmin` Container does not need port forwarding, but all other ports that the Container is using are now accessible to others on the same Layer2 network. This type of setup should only be used when your application requires that the Container has an IP address in the same Layer2 network such as application that use broadcast traffic for service discovery (in most cases such requirements can still be bypassed by using NAT).
