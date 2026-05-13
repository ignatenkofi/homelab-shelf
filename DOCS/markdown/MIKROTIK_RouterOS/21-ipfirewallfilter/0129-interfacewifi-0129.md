## `/interface/wifi` 

```
set wifi1 configuration.country=Latvia configuration.ssid=MikroTik_OWE security.authentication-types=owe
```

**==> picture [13 x 13] intentionally omitted <==**

802.11r (fast roaming) does not work over OWE networks. 

Resetting configuration 

1334 

WiFi interface configurations can be reset by using the 'reset' command. 

```
/interface/wifi reset wifi1
```

Physical interface MAC address to default can be reset by the command 'reset-mac-address'. 

```
/interface/wifi reset-mac-address wifi1
```
