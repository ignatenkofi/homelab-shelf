## MAC Telnet Server 

It is possible to set MAC Telnet access to specific interfaces that are a part of the interface list: 

```
[admin@device] /tool mac-server set allowed-interface-list=listBridge
[admin@device] /tool mac-server print
  allowed-interface-list: listBridge
```

In the example above, MAC Telnet is configured for the interface list "listBridge" and, as a result, MAC Telnet will only work via the interfaces that are members of the list (you can add multiple interfaces to the list). 

To disable MAC Telnet access, issue the command (set "allowed-interface-list" to "none"): 

```
[admin@device] /tool mac-server set allowed-interface-list=none
[admin@device] /tool mac-server print
  allowed-interface-list: none
```

You can check active MAC Telnet sessions (that the device accepted) with the command: 

```
[admin@device] > tool mac-server sessions print
Columns: INTERFACE, SRC-ADDRESS, UPTIME
#  INTERFACE  SRC-ADDRESS        UPTIME
0  ether5     64:D1:54:FB:E3:E6  17s
```
