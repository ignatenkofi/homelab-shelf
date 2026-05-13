## Option 2: Accessing certain addresses over the tunnel 

It is also possible to send only specific traffic over the tunnel by using the connection-mark parameter in the Mangle firewall. It works similarly as Option 1 - a dynamic NAT rule is generated based on configured connection-mark parameter under mode config. 

First of all, set the connection-mark under your mode config configuration. 

```
/ip ipsec mode-config
```

```
set [ find name=NordVPN ] connection-mark=NordVPN
```

When it is done, a NAT rule is generated with the dynamic address provided by the server: 

```
[admin@MikroTik] > /ip firewall nat print
Flags: X - disabled, I - invalid, D - dynamic
0  D ;;; ipsec mode-config
```

```
     chain=srcnat action=src-nat to-addresses=192.168.77.254 connection-mark=NordVPN
```

After that, it is possible to apply this connection-mark to any traffic using Mangle firewall. In this example, access to mikrotik.com and 8.8.8.8 is granted over the tunnel.
