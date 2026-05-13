## For Station device - 

Choose the same SSID, Password, frequency as the bridge device and choose station-bridge mode option that will act as a station for the setup, please see the example. 

Enable W60G interface after required parameters have been set. 

```
[admin@MikroTik] > interface w60g set wlan60-1 mode=station-bridge frequency=auto ssid=MySSID
password=choosepassword
[admin@MikroTik] > interface w60g print
Flags: X - disabled, R - running
```

```
0 X name="wlan60-1" mtu=1500 l2mtu=1600 mac-address=C4:AD:34:84:EE:5E arp=enabled arp-timeout=auto
region=no-region-set mode=station-bridge
```

```
ssid="MySSID" frequency=auto default-scan-list=58320,60480,62640,64800 password="choosepassword" tx-
sector=auto put-stations-in-bridge=bridge isolate-stations=yes
[admin@MikroTik] > /interface w60g enable wlan60-1
```
