## Static MDB entries 

Since RouterOS version 7.7, it is possible to create static MDB entries for IPv4 and IPv6 multicast groups. For example, to create a static MDB entry for multicast group 229.10.10.10 on ports ether2 and ether3 on VLAN 10, use the command below: 

523 

```
/interface bridge mdb
```

```
add bridge=bridge1 group=229.10.10.10 ports=ether2,ether3 vid=10
```
