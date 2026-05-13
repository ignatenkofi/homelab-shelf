## Local Forwarding Mode 

In this mode wireless interface on CAP behaves as a normal interface and takes part in normal data forwarding. Wireless interface will accept/pass data to networking stack on CAP. CAPsMAN will not participate in data forwarding and will not process any of data frames, it will only control interface configuration and client association process. 

Wireless interface on CAP will change its configuration to 'enabled' and its state and some relevant parameters (e.g. mac-address, arp, mtu) will reflect that of the interface on CAPsMAN. Note that wireless related configuration will not reflect actual interface configuration as applied by CAPsMAN: 

```
[admin@CAP] /interface wireless> pr
Flags: X - disabled, R - running
0  R ;;; managed by CAPsMAN
     ;;; channel: 5180/20-Ceee/ac, SSID: master, local forwarding
     name="wlan2" mtu=1500 mac-address=00:03:7F:48:CC:07 arp=enabled
     interface-type=Atheros AR9888 mode=ap-bridge ssid="merlin"
     frequency=5240 band=5ghz-a/n channel-width=20/40mhz-eC scan-list=default
     ...
```

Virtual-AP interfaces in local forwarding mode will appear as enabled and dynamic Virtual-AP interfaces: 

```
[admin@CAP] /interface> pr
Flags: D - dynamic, X - disabled, R - running, S - slave
#     NAME                                TYPE         MTU L2MTU  MAX-L2MTU
...
2  RS ;;; managed by CAPsMAN
      ;;; channel: 5180/20-Ceee/ac, SSID: master, local forwarding
      wlan2                               wlan        1500  1600
3 DRS ;;; managed by CAPsMAN
      ;;; SSID: slave, local forwarding
      wlan6                               wlan        1500  1600
...
[admin@CAP] /interface> wireless pr
Flags: X - disabled, R - running
...
2  R ;;; managed by CAPsMAN
     ;;; SSID: slave, local forwarding
     name="wlan6" mtu=1500 mac-address=00:00:00:00:00:00 arp=enabled
     interface-type=virtual-AP master-interface=wlan2
```

The fact that Virtual-AP interfaces are added as dynamic, somewhat limits static configuration possibilities on CAP for data forwarding, such as assigning addresses to Virtual-AP interface. This does not apply to master wireless interface. 

To overcome this it is possible to use the static-virtual setting on the CAP which will create Static Virtual Interfaces instead of Dynamic and allows the possibility to assign IP configuration to those interfaces. MAC address is used to remember each static-interface when applying the configuration from the CAPsMAN. If two or more static interfaces will have the same MAC address the configuration could be applied in random order. 

To facilitate data forwarding configuration, CAP can be configured with bridge to which interfaces are automatically added as ports when interfaces are enabled by CAPsMAN. This can be done in /interface wireless cap menu.
