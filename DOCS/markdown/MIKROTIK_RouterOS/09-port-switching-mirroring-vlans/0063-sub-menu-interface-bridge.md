## Sub-menu: `/interface bridge` 

**==> picture [516 x 285] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>igmp-querier  (none  | Shows a bridge port and source IP address from the detected IGMP querier. Only shows detected external IGMP querier, local<br>interface & IPv4  bridge IGMP querier (including IGMP proxy and PIM) will not be displayed. Monitoring value appears only when  igmp-snooping<br>address) is enabled.<br>mld-querier  (none  i| Shows a bridge port and source IPv6 address from the detected MLD querier. Only shows detected external MLD querier, local<br>nterface & IPv6  bridge MLD querier will not be displayed. Monitoring value appears only when igmp-snooping is enabled and the bridge has an<br>address) active IPv6 address.<br>multicast-router  (yes Shows if a multicast router is detected on the bridge interface. Monitoring value appears only when igmp-snooping is enabled.<br>| no)<br>[admin@MikroTik] /interface bridge monitor bridge1<br>                  state: enabled<br>    current-mac-address: 64:D1:54:C7:3A:59<br>            root-bridge: yes<br>         root-bridge-id: 0x8000.64:D1:54:C7:3A:59<br>         root-path-cost: 0<br>              root-port: none<br>             port-count: 3<br>  designated-port-count: 3<br>           fast-forward: no<br>       multicast-router: no<br>           igmp-querier: ether2 192.168.10.10<br>            mld-querier: ether2 fe80::e68d:8cff:fe39:3824<br>**----- End of picture text -----**<br>


To monitor the current status of bridge ports, use the `monitor` command.
