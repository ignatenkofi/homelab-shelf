## scan-list 

Interface scan-list is used in multiple modes that either gather information for list of channels (like interactive scan command) or selects channel to work on (like any of station modes or AP modes performing DFS). Interface scan-list can be configured with comma-separated list of the following items: 

default - default .11 channel list for given country and interface band and channel width; numeric frequency ranges in MHz; Advanced Channel, referred to by name; Advanced Channel list, referred to by list name. 

For example, to configure interface to scan 5180MHz, 5200MHz and 5220MHz at first using channel width 20MHz and then using channel width 10MHz, the following commands can be issued: 

```
[admin@MikroTik] /interface wireless> channels add frequency=5180 width=20 band=5ghz-a list=20MHz-list
[admin@MikroTik] /interface wireless> channels add frequency=5200 width=20 band=5ghz-a list=20MHz-list
[admin@MikroTik] /interface wireless> channels add frequency=5220 width=20 band=5ghz-a list=20MHz-list
[admin@MikroTik] /interface wireless> channels add frequency=5180 width=10 band=5ghz-a list=10MHz-list
[admin@MikroTik] /interface wireless> channels add frequency=5200 width=10 band=5ghz-a list=10MHz-list
[admin@MikroTik] /interface wireless> channels add frequency=5220 width=10 band=5ghz-a list=10MHz-list
[admin@MikroTik] /interface wireless> set wlan1 scan-list=20MHz-list,10MHz-list
```
