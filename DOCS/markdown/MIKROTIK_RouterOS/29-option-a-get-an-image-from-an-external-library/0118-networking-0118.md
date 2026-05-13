## Networking 

Add veth interface for the container: 

```
/interface/veth/add name=veth1 address=172.18.0.2/24 gateway=172.18.0.1
```

Create a bridge for the container, assign an IP network to it, and add veth to the bridge: 

```
/interface/bridge/add name=dockertb
```

```
/ip/address/add address=172.18.0.1/24 interface=dockertb
/interface/bridge/port add bridge=dockertb interface=veth1
```
