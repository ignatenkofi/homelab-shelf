## Result verification 

In RouterOS, add a new RADIUS client configuration: 

```
/radius/add service=login address=172.17.0.2 secret="client_password"
```

,where the `address` is the IP address of the veth3 interface, `secret` is the secret that we configured in the clients.conf file and `service` is the allowed service that you wish to use. 

Allow "login" with RADIUS users via the command: 

```
/user/aaa/set use-radius=yes
```

We have allowed the "login" service for the RADIUS and we can test it using ssh/winbox/webfig connection. For SSH test, issue the command (where you need to indicate the device's management IP and input bob's password "hello" after): 

```
/system/ssh 10.55.8.53 user=bob
```

You should be able to verify, that the terminal user changed from "admin@MikroTik" to "bob@MikroTik": 

1863 

```
[admin@MikroTik] > /system/ssh 10.55.8.53 user=bob
password:
hello
```

```
  MMM      MMM       KKK                          TTTTTTTTTTT      KKK
  MMMM    MMMM       KKK                          TTTTTTTTTTT      KKK
  MMM MMMM MMM  III  KKK  KKK  RRRRRR     OOOOOO      TTT     III  KKK  KKK
  MMM  MM  MMM  III  KKKKK     RRR  RRR  OOO  OOO     TTT     III  KKKKK
  MMM      MMM  III  KKK KKK   RRRRRR    OOO  OOO     TTT     III  KKK KKK
  MMM      MMM  III  KKK  KKK  RRR  RRR   OOOOOO      TTT     III  KKK  KKK
  MikroTik RouterOS 7.8alpha173 (c) 1999-2023       https://www.mikrotik.com/
Press F1 for help
[bob@MikroTik] >
```

If you issue the command `/user/active/print` : 

```
/user/active/print
Flags: R - RADIUS
Columns: WHEN, NAME, ADDRESS, VIA
#   WHEN                  NAME   ADDRESS     VIA
0   feb/16/2023 16:31:21  admin  xx.xx.xx.xx  winbox
1   feb/16/2023 16:38:46  admin  xx.xx.xx.xx  console
2 R feb/16/2023 16:38:53  bob    10.55.8.53  ssh
```

you will be able to verify, that a new user "bob" is "active" and has a flag "R" assigned, which indicates it is a RADIUS user. 

1864
