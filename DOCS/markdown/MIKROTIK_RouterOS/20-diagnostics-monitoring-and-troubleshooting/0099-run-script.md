## Run Script 

SNMP write allows running scripts on the router from the system script menu when you need to set value for the SNMP setting of the script. 

```
$ snmpset -c public -v 1 192.168.0.0 1.3.6.1.4.1.14988.1.1.8.1.1.3.X s 1
```

X , script number, numeration starts from 1; 

s 1 , snmpset command to set value, the value should not be equal to 0; 

The same command on RouterOS: 

```
/system script> print
Flags: I - invalid
0 name="test" owner="admin" policy=ftp,reboot,read,write,policy,
test,winbox,password,sniff last-started=jan/01/1970
01:31:57 run-count=23 source=:beep
```

```
/system script run 0
```
