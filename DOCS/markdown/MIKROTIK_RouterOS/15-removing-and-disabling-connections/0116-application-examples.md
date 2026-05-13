## Application Examples 

FTP service through SOCKS server 

Let us consider that we have a network 192.168.0.0/24 which is masqueraded, using a router with a public IP 10.1.0.104/24 and a private IP 192.168.0.1 /24. Somewhere in the network is an FTP server with IP address 10.5.8.8. We want to allow access to this FTP server for a client in our local network with IP address 192.168.0.2/24. 

We have already masqueraded our local network: 

```
[admin@MikroTik] ip firewall nat> print
Flags: X - disabled, I - invalid, D - dynamic
 0   chain=srcnat action=masquerade src-address=192.168.0.0/24
[admin@MikroTik] ip firewall nat>
```

And access to public FTP servers is denied in the firewall: 

```
[admin@MikroTik] ip firewall filter> print
Flags: X - disabled, I - invalid, D - dynamic
 0   chain=forward action=drop src-address=192.168.0.0/24 dst-port=21 protocol=tcp
[admin@MikroTik] ip firewall filter>
```

925 

We have to enable the SOCKS server: 

```
[admin@MikroTik] ip socks> set enabled=yes
[admin@MikroTik] ip socks> print
                    enabled: yes
                       port: 1080
    connection-idle-timeout: 2m
            max-connections: 200
[admin@MikroTik] ip socks>
```

Add access to a client with an IP address 192.168.0.2/32 to SOCKS access list, allow data transfer from FTP server to client (allow destination ports from 1024 to 65535 for any IP address), and drop everything else: 

```
[admin@MikroTik] ip socks access> add src-address=192.168.0.2 dst-port=21 \
\... action=allow
[admin@MikroTik] ip socks access> add dst-port=1024-65535 action=allow
[admin@MikroTik] ip socks access> add action=deny
[admin@MikroTik] ip socks access> print
Flags: X - disabled
 0   src-address=192.168.0.2 dst-port=21 action=allow
 1   dst-port=1024-65535 action=allow
 2   action=deny
[admin@MikroTik] ip socks access>
```

That's all - the SOCKS server is configured. To see active connections and data transmitted and received: 

```
[admin@MikroTik] ip socks connections> print
 # SRC-ADDRESS                DST-ADDRESS                TX         RX
 0 192.168.0.2:1238           10.5.8.8:21                1163       4625
 1 192.168.0.2:1258           10.5.8.8:3423              0          3231744
[admin@MikroTik] ip socks connections>
```

**==> picture [13 x 13] intentionally omitted <==**

In order to use the SOCKS proxy server, you have to specify its IP address and port in your FTP client. In this case, IP address would be 192.168.0.1 (local IP address of the router/SOCKS server) and TCP port 1080. 

926
