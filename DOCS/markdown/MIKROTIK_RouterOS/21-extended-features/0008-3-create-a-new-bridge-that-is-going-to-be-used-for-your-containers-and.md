## 3.  Create a new bridge that is going to be used for your Containers and assign the same IP address that was used for the veth interface's gateway: 

```
/interface/bridge/add name=containers
/ip/address/add address=172.17.0.1/24 interface=containers
```
