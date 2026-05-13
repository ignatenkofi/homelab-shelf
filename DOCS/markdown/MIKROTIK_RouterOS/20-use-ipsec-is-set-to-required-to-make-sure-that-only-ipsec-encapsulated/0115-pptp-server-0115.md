## PPTP Server 

On the other side we simply enable the PPTP server and create a PPP secret for a particular user: 

```
[admin@MikroTik] >  interface pptp-server server set enabled=yes
[admin@MikroTik] >  ppp secret add local-address=10.0.0.1 name=MT-User password=StrongPass profile=default-
encryption remote-address=10.0.0.5 service=pptp
[admin@MikroTik] >  interface pptp-server print
Flags: D - dynamic; R - running
Columns: NAME, USER, MTU, CLIENT-ADDRESS, UPTIME, ENCODING
#      NAME            USER     MTU  CLIENT-ADDRESS  UPTIM  ENCODING
0  DR  <pptp-MT-User>  MT-User  1450  192.168.51.3   44m8s  MPPE128 stateless
```

1262
