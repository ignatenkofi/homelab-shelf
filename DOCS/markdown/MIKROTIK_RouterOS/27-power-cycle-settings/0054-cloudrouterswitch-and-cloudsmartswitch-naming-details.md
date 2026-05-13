## CloudRouterSwitch and CloudSmartSwitch naming details 

CloudRouterSwitch (short version CRS, RouterOS device) CloudSmartSwitch (short version CSS, SwOS device) naming consists of: 

```
<3 digit number>-<list of ports>-<built-in wireless card>-<enclosure type>
```

3 digit number 1st digit stands for series 

1742 

2nd-3rd digit - total number of wired interfaces (Ethernet, SFP, SFP+) 

list of ports 

- -<n> F number of 100M Ethernet ports -<n> Fi number of 100M Ethernet ports with PoE-out injector -<n> Fp number of 100M Ethernet ports with controlled PoE-out -<n> Fr number of 100M Ethernet ports with Reverse PoE (PoE-in) -<n> G number of 1G Ethernet ports -<n> P number of 1G Ethernet ports with PoE-out -<n> C number of combo 1G Ethernet/SFP ports -<n> S number of 1G SFP ports 

- -<n> G+ number of 2.5G Ethernet ports -<n> P+ number of 2.5G Ethernet ports with PoE-out -<n> C+ number of combo 10G Ethernet/SFP ports -<n> S+ number of 10G SFP+ ports -<n> XG number of 5G/10G Ethernet ports -<n> XP number of 5G/10G Ethernet ports with PoE-out -<n> XC number of combo 10G/25G SFP+ ports -<n> XS number of 25G SFP+ ports -<n> Q+ number of 40G QSFP+ ports -<n> XQ number of 100G QSFP+ ports 

built-in wireless card - same as for RouterBOARD products. 

enclosure type - same as for RouterBOARD products. 

1743
