## Networking 

Add veth interface for the container: 

1860 

```
/interface/veth/add name=veth3 address=172.17.0.2/24 gateway=172.17.0.1
```

Create a bridge for the container, assign an IP network to it, and add veth to the bridge: 

```
/interface/bridge/add name=dockerfreeradius
```

```
/ip/address/add address=172.17.0.1/24 interface=dockerfreeradius
```

```
/interface/bridge/port add bridge=dockerfreeradius interface=veth3
```
