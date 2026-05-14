## SNMP OIDs for monitoring 

From RouterOS>=6.42rc6 SNMP support for W60G interface monitoring is added 

1432 

```
For main interfaces:
1.3.6.1.4.1.14988.1.1.1.8.1.2.1  integer  Mode
1.3.6.1.4.1.14988.1.1.1.8.1.3.1  string   SSID
1.3.6.1.4.1.14988.1.1.1.8.1.4.1  integer  Connected status
1.3.6.1.4.1.14988.1.1.1.8.1.5.1  string   Remote MAC
1.3.6.1.4.1.14988.1.1.1.8.1.6.1  integer  Frequency
1.3.6.1.4.1.14988.1.1.1.8.1.7.1  integer  MCS
1.3.6.1.4.1.14988.1.1.1.8.1.8.1  integer  Signal quality
1.3.6.1.4.1.14988.1.1.1.8.1.9.1  integer  tx-sector
1.3.6.1.4.1.14988.1.1.1.8.1.11.1 string   Sector info
1.3.6.1.4.1.14988.1.1.1.8.1.12.1 integer  RSSI
1.3.6.1.4.1.14988.1.1.1.8.1.13.1 gauge32  PHY rate
```
