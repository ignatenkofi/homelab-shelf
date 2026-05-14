## Get the script OID table 

```
$ snmpwalk -v2c -cpublic 192.168.88.1 1.3.6.1.4.1.14988.1.1.8
iso.3.6.1.4.1.14988.1.1.8.1.1.2.1 = STRING: "script1"
iso.3.6.1.4.1.14988.1.1.8.1.1.2.2 = STRING: "script2"
iso.3.6.1.4.1.14988.1.1.8.1.1.3.1 = INTEGER: 0
iso.3.6.1.4.1.14988.1.1.8.1.1.3.2 = INTEGER: 0
```

1816 

To run the script use table 18 

```
$ snmpget -v2c -cpublic 192.168.88.1 1.3.6.1.4.1.14988.1.1.18.1.1.2.2
iso.3.6.1.4.1.14988.1.1.18.1.1.2.2 = STRING: "output"
```

1817
