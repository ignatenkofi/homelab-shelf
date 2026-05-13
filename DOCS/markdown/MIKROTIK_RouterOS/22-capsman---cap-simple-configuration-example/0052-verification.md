## Verification 

On a successful connection, both the AP and the Station should display a new entry in the "Registration" table: 

```
/interface/wifi/registration-table/print
Flags: A - AUTHORIZED
Columns: INTERFACE, SSID, MAC-ADDRESS, UPTIME, LAST-ACTIVITY, SIGNAL, AUTH-TYPE, BAND
#   INTERFACE  SSID        MAC-ADDRESS        UPTIME    LAST-ACTIVITY  SIGNAL  AUTH-TYPE  BAND
0 A wifi1      input_SSID  XX:YY:ZZ:AA:30:6E  6h24m21s  0ms            -72     wpa2-psk   5ghz-ax
```

You can also check, via the CPE, whether it properly sees/recognizes the AP using the "scan" command: 

1371 

```
/interface/wifi scan [find where name=wifi1]
Flags: A - ACTIVE
Columns: ADDRESS, SSID, CHANNEL, SECURITY, SIGNAL, STA-COUNT
  ADDRESS            SSID               CHANNEL           SECURITY                              SIGNAL  STA-
COUNT
A XX:YY:ZZ:AA:F4:28  SSID_Y             5620/ax           WPA2-PSK/WPA3-PSK                     -60
0
A XX:YY:ZZ:BB:0B:DA  SSID_X             5745/ax/Ce        WPA3-PSK                              -68
0
A XX:YY:ZZ:CC:0B:DA  input_SSID         5745/ax/Ce        WPA2-PSK                              -68
0
A XX:YY:ZZ:DD:0B:DA                     5745/ax/Ce        WPA2-PSK                              -68
0
```

1372
