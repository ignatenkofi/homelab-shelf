## Option matcher examples 

Match dhcp1 server clients by exact Vendor class identifier (DHCP option 60) and assign address from the pool1: 

```
/ip dhcp-server matcher
```

```
add address-pool=pool1 code=60 matching-type=exact name=test1 server=dhcp1 value=android-dhcp-11
```

Match clients on all DHCP servers by exact Client Id (DHCP option 61) configured as hex value and assign address from the pool2: 

```
/ip dhcp-server matcher
```

```
add address-pool=pool2 code=61 matching-type=exact name=test2 server=all value=0x016c3b6bed8364
```

Match dhcp2 server clients partially by Hostname (DHCP option 12) and assign address from the pool3: 

```
/ip dhcp-server matcher
```

```
add address-pool=pool3 code=12 matching-type=substring name=test3 server=dhcp2 value=MikroTik
```
