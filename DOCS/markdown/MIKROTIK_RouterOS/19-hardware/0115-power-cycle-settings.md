## Power-cycle settings 

RouterOS provides a possibility to monitor PD using a ping, and power-cycle a PoE-Out port when the host does not respond. power-cycle-ping feature can be enabled under `/interface ethernet poe` menu. 

**==> picture [509 x 226] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>power-cycle- Enables ping watchdog, power-cycles port if a host does not respond to ICMP or MAC-Telnet packets.<br>ping-enabled  (<br>yes | no;<br>Default: no )<br>power-cycle- An address which will be monitored. Since RouterOS 6.46beta16, an active route towards PD is required in case an IP address is<br>ping-address  (I configured, so make sure PSE can reach the PD. In case the MAC address is specified, PSE will send MAC-Telnet ping requests<br>Pv4 | IPv6 |  only from a specified ethernet interface. When configuring a bridge vlan-filtering or some way of VLAN switching, it is recommended<br>MAC; Default:  to use the IP address for monitoring your PD.<br>)<br>power-cycle- If the host does not respond for more than <timeout> period of time, then PoE-Out port is switched off for 5s.<br>ping-timeout  (ti<br>me:0..1h |;<br>Default: 5s )<br>power-cycle- Disables PoE-Out power for 5s between the specified intervals. Not related with the power-cycle-ping feature.<br>interval  (time|<br>any; Default: )<br>**----- End of picture text -----**<br>

If power-cycle is enabled, `/interface ethernet poe monitor` will show the actual status of the host and time when power cycle will be performed [1] 

**==> picture [13 x 13] intentionally omitted <==**

power-cycle-host-alive: <YES/NO> (Shows if monitored host is reachable) power-cycle-after:<TIME> (Shows time, after which the port will be power-cycled)
