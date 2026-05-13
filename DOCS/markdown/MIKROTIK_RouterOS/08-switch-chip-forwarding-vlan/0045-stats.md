## Stats 

**==> picture [516 x 458] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>ipv4- The total number of IPv4 routes handled by the switch driver.<br>routes-<br>total<br>ipv4- The number of hardware-offloaded IPv4 routes (a.k.a. hardware routes)<br>routes-hw<br>ipv4- The number of IPv4 routes redirected to the CPU (a.k.a. software routes)<br>routes-cpu<br>ipv4- Shortest Hardware Prefix (SHWP) for IPv4. If the entire IPv4 routing table does not fit into the hardware memory, partial offloading is<br>shortest- applied, where the longest prefixes are hw-offloaded while the shorter ones are redirected to the CPU. This field shows the shortest route<br>hw-prefix prefix (/x) that is offloaded to the hardware memory. All prefixes shorter than this are processed by the CPU. " ipv4-shortest-hw-<br>prefix=0 " means the entire IPv4 routing table is offloaded to the hardware memory.<br>ipv4-hosts The number of hardware-offloaded IPv4 hosts (/32 routes)<br>ipv6- The total number of IPv6 routes handled by the switch driver.<br>routes-<br>total  [1]<br>ipv6- The number of hardware-offloaded IPv6 routes (a.k.a. hardware routes)<br>routes-hw [1]<br>ipv6- The number of IPv6 routes redirected to the CPU (a.k.a. software routes)<br>routes-cpu<br>1<br>ipv6- Shortest Hardware Prefix (SHWP) for IPv6. If the entire IPv6 routing table does not fit into the hardware memory, partial offloading is<br>shortest- applied, where the longest prefixes are hw-offloaded while the shorter ones are redirected to the CPU. This field shows the shortest route<br>hw-prefix  [1] prefix (/x) that is offloaded to the hardware memory. All prefixes shorter than this are processed by the CPU. " ipv6-shortest-hw-<br>prefix=0 " means the entire IPv6 routing table is offloaded to the hardware memory.<br>ipv6-hosts  The number of hardware-offloaded IPv6 hosts (/128 routes)<br>1<br>route- The number of routes in the queue for processing by the switch chip driver. Under normal working conditions, this field is 0, meaning that<br>queue- all routes are processed by the driver.<br>size<br>nexthop- The nexthop capacity.<br>cap<br>**----- End of picture text -----**<br>


437 

nexthopThe number of currently used nexthops. usage vxlan-mtuThe number of dropped VXLAN packets due to exceeded interface MTU settings. packetdrop fasttrackThe number of hardware-offloaded FastTrack connections. ipv4conns[2] fasttrackWhen the hardware memory for storing FastTrack is full, this field shows the minimum speed (in bytes per second) of a hw-offloaded hw-minFastTrack connection. Slower connections are routed by the CPU. speed[2] 

1 IPv6 stats appear only when IPv6 hardware routing is enabled ( _`ipv6-hw=yes`_ ) 

> 2 FastTrack stats appear only when hardware offloading of FastTrack connections is enabled (fasttrack-hw _`=yes`_ )
