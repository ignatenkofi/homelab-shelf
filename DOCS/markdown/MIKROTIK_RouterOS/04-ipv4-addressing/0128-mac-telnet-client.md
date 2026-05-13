## MAC Telnet Client 

When MAC Telnet Server is enabled, you can use another RouterOS device to connect to the server using the mac-telnet client: 

220 

```
[admin@device2] > tool mac-telnet B8:69:F4:7F:F2:E7
Login: admin
Password:
Trying B8:69:F4:7F:F2:E7...
Connected to B8:69:F4:7F:F2:E7
```

```
  MMM      MMM       KKK                          TTTTTTTTTTT      KKK
  MMMM    MMMM       KKK                          TTTTTTTTTTT      KKK
  MMM MMMM MMM  III  KKK  KKK  RRRRRR     OOOOOO      TTT     III  KKK  KKK
  MMM  MM  MMM  III  KKKKK     RRR  RRR  OOO  OOO     TTT     III  KKKKK
  MMM      MMM  III  KKK KKK   RRRRRR    OOO  OOO     TTT     III  KKK KKK
  MMM      MMM  III  KKK  KKK  RRR  RRR   OOOOOO      TTT     III  KKK  KKK
  MikroTik RouterOS 7.1rc3 (c) 1999-2021       https://www.mikrotik.com/
Press F1 for help
[admin@device] >
```

Change the MAC address accordingly (to your setup) and you should get into the server's CLI (as shown in the example above). 

**==> picture [13 x 13] intentionally omitted <==**

By default, a MAC Telnet client attempts to reach the destination through all active interfaces. This can generate unwanted traffic. To restrict a MAC Telnet client to a specific interface, use the `interface` property (available since RouterOS v7.22). For example: `/tool/mac-telnet 00:11:22:33:44:55 interface=ether1`
