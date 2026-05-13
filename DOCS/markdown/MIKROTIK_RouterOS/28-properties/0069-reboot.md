## Reboot 

It's possible to reboot the router with SNMP set command, you need to set the value for reboot SNMP settings, which is not equal to 0. 

```
$ snmpset -c public -v 1 192.168.0.0 1.3.6.1.4.1.14988.1.1.7.1.0 s 1
```

1.3.6.1.4.1.14988.1.1.7.1.0 , SNMP value for the router reboot; 

s 1 , snmpset command to set value, value should not be equal to 0; 

Reboot SNMPset command is equal to the RouterOS command: 

```
/system reboot
```
