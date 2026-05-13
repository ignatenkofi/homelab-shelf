## Setup example 

The goal of this example is to get Layer 3 connectivity between two remote sites over the internet 

**==> picture [505 x 271] intentionally omitted <==**

We have two sites, Site1 with local network range 10.1.101.0/24 and Site2 with local network range 10.1.202.0/24. 

The first step is to create GRE tunnels. A router on site 1: 

```
/interface gre add name=myGre remote-address=192.168.90.1 local-address=192.168.80.1
```

A router on site 2: 

```
/interface gre add name=myGre remote-address=192.168.80.1 local-address=192.168.90.1
```

As you can see tunnel configuration is quite simple. 

**==> picture [13 x 13] intentionally omitted <==**

In this example, a keepalive is not configured, so tunnel interface will have a running flag even if remote tunnel end is not reachable 

Now we just need to set up tunnel addresses and proper routing. A router on site 1: 

1184 

```
/ip address add address=172.16.1.1/30 interface=myGre
/ip route add dst-address=10.1.202.0/24 gateway=172.16.1.2
```
