## Specify the IP address and port of the host, which will receive Traffic-Flow packets: 

```
[admin@MikroTik] ip traffic-flow target> add dst-address=192.168.0.2 port=2055 version=9
[admin@MikroTik] ip traffic-flow target> print
Flags: X - disabled
 #   SRC-ADDRESS       DST-ADDRESS        PORT     VERSION
 0   0.0.0.0           192.168.0.2        2055     9
[admin@MikroTik] ip traffic-flow target>
```

Now the router starts to send packets with Traffic-Flow information. 

**==> picture [13 x 13] intentionally omitted <==**
