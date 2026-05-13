## Bonding monitoring 

Since RouterOS 6.48 version, it is possible to monitor the bonding interface and bonding ports. For the `802.3ad` bonding mode, more detailed monitoring options are available. 

```
/interface bonding monitor [find]
                      mode: 802.3ad           active-backup
              active-ports: ether4            ether6
                            ether5
            inactive-ports:                   ether7
            lacp-system-id: CC:2D:E0:11:22:33
      lacp-system-priority: 65535
    lacp-partner-system-id: B8:69:F4:44:55:66
```

**==> picture [516 x 119] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>mode  (802.3ad | active-backup | balance-alb | balance-rr | balance-tlb | balance-xor |  Used bonding mode<br>broadcast)<br>active-ports  (interface) Shows the active bonding ports<br>inactive-ports  (interface) Shows the inactive bonding ports (e.g. a disabled or backup<br>interface)<br>lacp-system-id  (MAC address) Shows the local LACP system ID<br>**----- End of picture text -----**<br>


768 

lacp-system-priority (integer) lacp-partner-system-id (MAC address) 

Shows the local LACP priority Shows the partner LACP system ID 

To monitor individual bonding ports, use a `monitor-slaves` command. 

```
/interface bonding monitor-slaves bond1
```

```
Flags: A - active, P - partner
```

```
 AP port=ether4 key=17 flags="A-GSCD--" partner-sys-id=D4:CA:6D:12:06:65 partner-sys-priority=65535 partner-
key=9 partner-flags="A-GSCD--"
```

```
 AP port=ether5 key=17 flags="A-GSCD--" partner-sys-id=D4:CA:6D:12:06:65 partner-sys-priority=65535 partner-
key=9 partner-flags="A-GSCD--"
```

**==> picture [516 x 312] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>port  (interface) Used bonding port<br>key  (integer) Shows the local LACP aggregation key. The lower 6 bits are automatically assigned based on individual port link speed and duplex.<br>The upper 10 bits can be manually specified using the  lacp-user-key  setting (available only since RouterOS v7.3).<br>flags  (string) Shows the local LACP flags:<br>A - activity (link is active, otherwise passive)<br>T - timeout (link is using short 1-second timeout, otherwise using 30-second timeout)<br>G - aggregation (link can be aggregatable)<br>S - synchronization (link is synchronized)<br>C - collecting (link is able to collect incoming frames)<br>D - distributing (link is able to distribute outgoing frames)<br>F - defaulted (link is using defaulted partner information, indicated that no LACPDU has been received from the partner)<br>E - expired (link has expired state)<br>partner-sys-id Shows the partner LACP system ID<br>(MAC address)<br>partner-sys- Shows the partner LACP priority<br>priority  (integer<br>)<br>partner-key  (in Shows the partner LACP aggregation key<br>teger)<br>partner-flags  ( Shows the partner LACP flags<br>string)<br>**----- End of picture text -----**<br>
