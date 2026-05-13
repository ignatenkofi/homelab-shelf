## (Optional) Accounting configuration 

To keep track of every user's uptime, download and upload statistics, RADIUS accounting can be used. By default RADIUS accounting is already enabled for IPsec, but it is advised to configure Interim Update timer that sends statistic to the RADIUS server regularly. If the router will handle a lot of simultaneous sessions, it is advised to increase the update timer to avoid increased CPU usage. 

```
/ip ipsec settings
set interim-update=1m
```
