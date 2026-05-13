## System Identity 

It's possible to change router system identity by SNMP set command. 

```
$ snmpset -c public -v 1 192.168.0.0 1.3.6.1.2.1.1.5.0 s New_Identity
```

snmpset - SNMP application used for SNMP SET requests to set information on a network entity; public - router's community name; 

- 192.168.0.0 - IP address of the router; 

1.3.6.1.2.1.1.5.0 - SNMP value for router's identity; 

SNMPset command above is equal to the RouterOS command: 

1815 

```
/system identity set identity=New_Identity
```
