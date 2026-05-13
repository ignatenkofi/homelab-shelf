## `/ip firewall filter` 

```
add action=fasttrack-connection chain=forward comment=FastTrack connection-state=established,related
add action=accept chain=forward comment="Established, Related" connection-state=established,related
add action=drop chain=forward comment="Drop invalid" connection-state=invalid log=yes log-prefix=invalid
add action=drop chain=forward comment="Drop tries to reach not public addresses from LAN" dst-address-
list=not_in_internet in-interface=bridge log=yes log-prefix=!public_from_LAN out-interface=!bridge
add action=drop chain=forward comment="Drop incoming packets that are not NAT`ted" connection-nat-state=!dstnat
connection-state=new in-interface=ether1 log=yes log-prefix=!NAT
```

```
add action=jump chain=forward protocol=icmp jump-target=icmp comment="jump to ICMP filters"
```

```
add action=drop chain=forward comment="Drop incoming from internet which is not public IP" in-interface=ether1
log=yes log-prefix=!public src-address-list=not_in_internet
```

```
add action=drop chain=forward comment="Drop packets from LAN that do not have LAN IP" in-interface=bridge
log=yes log-prefix=LAN_!LAN src-address=!192.168.88.0/24
```
