## frequency 

To use particular Advanced Channel for wireless interface (applies to modes that make use of interface frequency setting) specify channel name in interface frequency setting. For example, to configure interface to operate with center frequency 5500MHz and channel width 14MHz, use the following commands: 

```
[admin@MikroTik] /interface wireless> channels add name=MYCHAN frequency=5500 width=14 band=5ghz-onlyn
 list=MYLIST
```

```
[admin@MikroTik] /interface wireless> set wlan1 frequency=MYCHAN
```

1407
