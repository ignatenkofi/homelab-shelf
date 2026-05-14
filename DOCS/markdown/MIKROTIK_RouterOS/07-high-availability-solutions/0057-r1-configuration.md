## R1 configuration: 

```
/ip address add address=192.168.1.10/24 interface=ether1
```

```
/interface vrrp add interface=ether1 vrid=49 priority=254
```

```
/ip address add address=192.168.1.1/32 interface=vrrp1
```

R2 configuration: 

792 

```
/ip address add address=192.168.1.20/24 interface=ether1
/interface vrrp add interface=ether1 vrid=49
/ip address add address=192.168.1.1/32 interface=vrrp1
```
