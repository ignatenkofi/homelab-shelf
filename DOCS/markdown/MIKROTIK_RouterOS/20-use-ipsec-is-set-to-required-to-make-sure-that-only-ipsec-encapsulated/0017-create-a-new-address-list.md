## Create a new address list: 

```
/ip firewall address-list
add address=mikrotik.com list=VPN
add address=8.8.8.8 list=VPN
```

Apply connection-mark to traffic matching the created address list: 

```
/ip firewall mangle
```

```
add action=mark-connection chain=prerouting dst-address-list=VPN new-connection-mark=NordVPN passthrough=yes
```

**==> picture [13 x 13] intentionally omitted <==**

It is also possible to combine both options (1 and 2) to allow access to specific addresses only for specific local addresses/networks 

1231
