## SNMP write 

SNMP write allows changing router configuration with SNMP requests. Consider securing access to the router or to router's SNMP, when SNMP and writeaccess are enabled. 

To change settings by SNMP requests, use the command below to allow SNMP to write for the selected community. 

```
/snmp community set <number> write-access=yes
```
