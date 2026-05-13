## CAPsMAN: 

```
#create a security profile
/interface wifi security
```

```
add authentication-types=wpa3-psk name=sec1 passphrase=HaveAg00dDay
```

```
#create configuraiton profiles to use for provisioning
/interface wifi configuration
add country=Latvia name=5ghz security=sec1 ssid=CAPsMAN_5
add name=2ghz security=sec1 ssid=CAPsMAN2
add country=Latvia name=5ghz_v security=sec1 ssid=CAPsMAN5_v
```

```
#configure provisioning rules, configure band matching as needed
/interface wifi provisioning
```

```
add action=create-dynamic-enabled master-configuration=5ghz slave-configurations=5ghz_v supported-bands=\
    5ghz-n
```

```
add action=create-dynamic-enabled master-configuration=2ghz supported-bands=2ghz-n
```

```
#enable CAPsMAN service
/interface wifi capsman
set ca-certificate=auto enabled=yes
```

CAP: 

1344 

```
#enable CAP service, in this case CAPsMAN is on same LAN, but you can also specify "caps-man-addresses=x.x.x.x"
here
```

```
/interface/wifi/cap set enabled=yes
```

```
#set configuration.manager= on the WiFi interface that should act as CAP
```

```
/interface/wifi/set wifi1,wifi2 configuration.manager=capsman-or-local
```

**==> picture [13 x 13] intentionally omitted <==**

- If the CAP is hAP ax2 or hAP ax3, it is strongly recommended to enable RSTP in the bridge configuration, on the CAP 

configuration.manager should only be set on the CAP device itself, don't pass it to the CAP or configuration profile that you provision. 

**==> picture [13 x 13] intentionally omitted <==**

The interface that should act as CAP needs additional configuration under "interface/wifi/set wifiX configuration.manager="
