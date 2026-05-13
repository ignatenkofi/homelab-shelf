## Add IP address on wlan1 interface. 

Create wireless security-profile compatible with R2 wlan2. 

```
[admin@R4] >
/ip address
add address=192.168.2.4/24 interface=wlan1
```

```
/interface wireless
```

```
set [ find default-name=wlan1 ] disabled=no security-profile=vlan222
```

1534
