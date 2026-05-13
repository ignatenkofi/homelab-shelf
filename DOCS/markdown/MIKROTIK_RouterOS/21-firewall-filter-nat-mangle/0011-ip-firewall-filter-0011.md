## `/ip firewall filter` 

```
add action=accept chain=input comment="allow WireGuard traffic" src-address=192.168.100.0/24 place-before=1
```

Or simply add the WireGuard interface to "LAN" interface list. 

```
/interface list member
add interface=wireguard1 list=LAN
```
