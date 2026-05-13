## Configuration 

R1 configuration: 

```
/ip address add address=192.168.1.1/24 interface=ether1
/interface vrrp add interface=ether1 vrid=49 priority=254
/interface vrrp add interface=ether1 vrid=77
/ip address add address=192.168.1.253/32 interface=vrrp1
/ip address add address=192.168.1.254/32 interface=vrrp2
```

R2 configuration: 

794 

```
/ip address add address=192.168.1.2/24 interface=ether1
```

```
/interface vrrp add interface=ether1 vrid=49
```

```
/interface vrrp add interface=ether1 vrid=77 priority=254
```

```
/ip address add address=192.168.1.253/32 interface=vrrp1
/ip address add address=192.168.1.254/32 interface=vrrp2
```
