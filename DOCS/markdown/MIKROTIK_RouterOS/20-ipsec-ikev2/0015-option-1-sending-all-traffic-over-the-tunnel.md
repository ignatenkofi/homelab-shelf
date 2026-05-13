## Option 1: Sending all traffic over the tunnel 

1230 

In this example, we have a local network 10.5.8.0/24 behind the router and we want all traffic from this network to be sent over the tunnel. First of all, we have to make a new IP/Firewall/Address list which consists of our local network. 

```
/ip firewall address-list
```

```
add address=10.5.8.0/24 list=local
```

It is also possible to specify only single hosts from which all traffic will be sent over the tunnel. Example: 

```
/ip firewall address-list
add address=10.5.8.120 list=local
add address=10.5.8.23 list=local
```

When it is done, we can assign newly created IP/Firewall/Address list to mode config configuration. 

```
/ip ipsec mode-config
```

```
set [ find name=NordVPN ] src-address-list=local
```

Verify correct source NAT rule is dynamically generated when the tunnel is established. 

```
[admin@MikroTik] > /ip firewall nat print
```

```
Flags: X - disabled, I - invalid, D - dynamic
0  D ;;; ipsec mode-config
```

```
     chain=srcnat action=src-nat to-addresses=192.168.77.254 src-address-list=local dst-address-list=!local
```

**==> picture [13 x 13] intentionally omitted <==**

Warning 

Make sure the dynamic mode config address is not a part of the local network. 

**==> picture [13 x 13] intentionally omitted <==**

It is also possible to combine both options (1 and 2) to allow access to specific addresses only for specific local addresses/networks
