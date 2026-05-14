## Sub-menu: `/interface vxlan fdb` 

**==> picture [337 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>interface (read-only: name) Name of the VXLAN interface.<br>mac-address (read-only: MAC address) MAC address.<br>remote-ip (read-only: IPv4 | IPv6 address) The IPv4 or IPv6 destination address of remote VTEP.<br>**----- End of picture text -----**<br>

507 

```
[admin@MikroTik] > /interface vxlan fdb print
```

```
 0 remote-ip=2001::2 mac-address=56:FF:AA:1A:72:33 interface=vxlan1
```

```
 1 remote-ip=2002::2 mac-address=AE:EC:C4:12:8B:B9 interface=vxlan1
```

```
 2 remote-ip=192.168.10.20 mac-address=FE:AF:58:31:A7:B6 interface=vxlan2
```
