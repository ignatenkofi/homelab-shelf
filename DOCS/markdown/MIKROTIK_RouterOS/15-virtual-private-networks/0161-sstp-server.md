## SSTP Server 

We will configure PPP secret for a particular user, afterwards simply enable an SSTP server: 

```
[admin@MikroTik] > ppp secret add local-address=10.0.0.1 name=MT-User password=StrongPass remote-address=10.
0.0.5 service=sstp
[admin@MikroTik] > interface sstp-server server set default-profile=default-encryption enabled=yes
[admin@MikroTik] > interface sstp-server server print
                    enabled: yes
                       port: 443
                    max-mtu: 1500
                    max-mru: 1500
                       mrru: disabled
          keepalive-timeout: 60
            default-profile: default-encryption
             authentication: pap,chap,mschap1,mschap2
                certificate: none
  verify-client-certificate: no
                        pfs: no
                tls-version: any
```

**==> picture [13 x 13] intentionally omitted <==**

In P2P setups network address will be same with other endpoint local address. 

**==> picture [13 x 13] intentionally omitted <==**

As with any other ppp tunnel, SSTP also supports BCP which allows it to bridge SSTP tunnel with a local interface. For example in setups where routers are connected to Internet through ether1, workstations and laptops are connected to ether2. Both local networks are routed through SSTP client, and they are not in the same broadcast domain BCP is used. 

1267
