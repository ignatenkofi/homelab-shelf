## MAC WinBox Server 

Same as with MAC Telnet, it is possible to set MAC WinBox access to specific interfaces that are a part of the interface list: 

```
[admin@device] > tool mac-server mac-winbox set allowed-interface-list=listBridge
[admin@device] > tool mac-server mac-winbox print
  allowed-interface-list: listBridge
```

In the example above, MAC WinBox access is configured for the interface list "listBridge" and, as a result, MAC WinBox will only work via the interfaces that are members of the list. 

221 

To disable MAC WinBox access, issue the command (set "allowed-interface-list" to "none"): 

```
[admin@device] > tool mac-server mac-winbox set allowed-interface-list=none
```

```
[admin@device] > tool mac-server mac-winbox print
  allowed-interface-list: none
```
