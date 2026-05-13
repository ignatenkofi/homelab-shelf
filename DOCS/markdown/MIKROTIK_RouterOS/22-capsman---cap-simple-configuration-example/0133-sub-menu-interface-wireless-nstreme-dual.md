## Sub-menu: `/interface wireless nstreme-dual` 

Two radios in nstreme-dual-slave mode can be grouped together to make nstreme2 Point-to-Point connection. To put wireless interfaces into a nstreme2 group, you should set their mode to nstreme-dual-slave. Many parameters from /interface wireless menu are ignored, using the nstreme2, except: 

frequency-mode country antenna-gain tx-power tx-power-mode antenna-mode 

**==> picture [504 x 482] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>arp  (disabled | enabled | proxy-arp | reply-only;  Read more >><br>Default: enabled )<br>comment  (string; Default: ) Short description of an entry<br>disable-csma  (yes | no; Default: no ) Disable CSMA/CA (better performance)<br>disable-running-check  (yes | no; Default: no ) Whether the interface should always be treated as running even if there is no connection to a<br>remote peer<br>disabled  (yes | no; Default: yes )<br>framer-limit  (integer [64..4000]; Default: 2560 ) Maximal frame size<br>framer-policy  (best-fit | exact-size | none; Default: The method how to combine frames. A number of frames may be combined into one bigger<br>none ) one to reduce the amout of protocol overhead (and thus increase speed). The card are not<br>waiting for frames, but in case a number packets are queued for transmitting, they can be<br>combined. There are several methods of framing:<br>none  - do nothing special, do not combine packets<br>best-fit  - put as much packets as possible in one frame, until the framer-limit limit is met,<br>but do not fragment packets<br>exact-size  - put as much packets as possible in one frame, until the framer-limit limit is<br>met, even if fragmentation will be needed (best performance)<br>ht-channel-width  (2040mhz | 20mhz | 40mhz;<br>Default: 20mhz )<br>ht-guard-interval  (both | long | short; Default: long )<br>ht-rates  (list of rates [1,2,3,4,5,6,7,8]; Default: 1,2,<br>3,4,5,6,7,8 )<br>ht-streams  (both | double | single; Default: single )<br>l2mtu  (integer [0..65536]; Default: )<br>mtu  (integer [0..65536]; Default: 1500 )<br>name  (string; Default: ) Name of an entry<br>rates-a/g  (list of rates [6Mbps,9Mbps, 12Mbps,  Rates to be supported in 802.11a or 802.11g standard<br>18Mbps, 24Mbps, 36Mbps, 48Mbps, 54Mbps];<br>Default:  6Mbps,9Mbps,12Mbps, 18Mbps,<br>24Mbps, 36Mbps, 48Mbps, 54Mbps )<br>**----- End of picture text -----**<br>


1409 

**==> picture [504 x 232] intentionally omitted <==**

**----- Start of picture text -----**<br>
rates-b  (list of rates [1Mbps, 2Mbps, 5.5Mbps,  Rates to be supported in 802.11b standard<br>11Mbps]; Default: 1Mbps, 2Mbps, 5.5Mbps,<br>11Mbps )<br>remote-mac  (MAC; Default: 00:00:00:00:00:00 ) Which MAC address to connect to (this would be the remote receiver card's MAC address)<br>rx-band  (2ghz-b | 2ghz-g | 2ghz-n | 5ghz-a | 5ghz- Operating band of the receiving radio<br>n; Default: )<br>rx-channel-width  (10mhz; Default: 20mhz )<br>rx-frequency  (integer [0..4294967295]; Default: ) RX card operation frequency in Mhz.<br>rx-radio  (string; Default: ) Name of the interface used for receive.<br>tx-band  (2ghz-b | 2ghz-g | 2ghz-n | 5ghz-a | 5ghz- Operating band of the transmitting radio<br>n; Default: )<br>tx-channel-width  (10mhz; Default: 20mhz )<br>tx-frequency  (integer [0..4294967295]; Default: ) TX card operation frequency in Mhz.<br>tx-radio  (string; Default: ) Name of the interface used for transmit.<br>**----- End of picture text -----**<br>


Warning: WDS cannot be used on Nstreme-dual links. 

Note: The difference between tx-freq and rx-freq should be about 200MHz (more is recommended) because of the interference that may occur! 

Note: You can use different bands for rx and tx links. For example, transmit in 2ghz-g and receive data, using 2ghz-b band.
