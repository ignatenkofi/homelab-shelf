## To enable the UPnP feature: 

```
[admin@MikroTik] ip upnp> set enable=yes
[admin@MikroTik] ip upnp> print
                             enabled: yes
    allow-disable-external-interface: yes
                     show-dummy-rule: yes
[admin@MikroTik] ip upnp>
```

Now, all we have to do is to add interfaces: 

```
[admin@MikroTik] ip upnp interfaces> add interface=ether1 type=external
[admin@MikroTik] ip upnp interfaces> add interface=ether2 type=internal
[admin@MikroTik] ip upnp interfaces> print
Flags: X - disabled
  #   INTERFACE TYPE
  0 X ether1    external
  1 X ether2    internal
[admin@MikroTik] ip upnp interfaces> enable 0,1
```

Now once the client from the internal interface side sends UPnP request, dynamic NAT rules will be created on the router, example rules could look something similar to these: 

```
[admin@MikroTik] > ip firewall nat print
Flags: X - disabled, I - invalid, D - dynamic
```

```
0 chain=srcnat action=masquerade out-interface=ether1
```

```
1 D ;;; upnp 192.168.88.10: ApplicationX
chain=dstnat action=dst-nat to-addresses=192.168.88.10 to-ports=55000 protocol=tcp
dst-address=10.0.0.1 in-interface=ether1 dst-port=55000
```

```
2 D ;;; upnp 192.168.88.10: ApplicationX
chain=dstnat action=dst-nat to-addresses=192.168.88.10 to-ports=55000 protocol=udp
dst-address=10.0.0.1 in-interface=ether1 dst-port=55000
```

752
