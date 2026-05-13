## Port Settings 

PoE-Out can be configured under the menu. Each port can be controlled independently. 

**==> picture [509 x 291] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  () Name of an interface<br>poe-out  (auto-on |  Specifies PoE-Out state<br>forced-on | off; Default: a<br>uto-on ) auto-on - the board will attempt to detect if power can be applied to the port. For powering there should be resistance<br>in the range from 3kΩ to 26.5kΩ<br>forced-on - detection range is removed. As a result power to PD will be provided through B (alt) pairs and power over<br>Ethernet will be always on<br>forced-on-a - same as forced-on but the power to PD will be provided through A (main) pairs instead of B pairs.<br>(Available only on PSE that support 802.3bt PoE-Out)<br>forced-on-bt - detection range is removed. Power to PD will be provided through all 4 power pairs and power over<br>Ethernet will be always on. (Available only on PSE that support 802.3bt PoE-Out)<br>off - all detection and power is turned off for this port<br>Note:  Short-circuit and overload protection is always on independently from the selected PoE-Out state.<br>poe-priority  (integer:0.. poe-priority specifies the importance of PoE-Out ports, in cases when a total PoE-Out limit is reached, interface with the<br>99 | any; Default: 10 ) lowest port priority will be powered off first.<br>Highest priority is 0, the lowest priority is 99. If there are 2 or more ports with the same priority then port with the smallest<br>port number will have a higher priority.<br>Every 6 seconds ports will be checked for a possibility to provide PoE-Out if it was turned off due to port priority.<br>**----- End of picture text -----**<br>


1729 

poe-voltage (auto | low | A feature that allows us to manually switch between two voltage outputs on PoE-Out ports. It will take effect only on PSE high; Default: auto ) with switchable voltage modes (CRS112-8P-4S-IN, CRS328-24P-4S+RM, netPower 16P, CRS354-48P-4S+2Q+RM). poe-lldp-enabled ( yes / Link Layer Discovery Protocol (LLDP) is a layer-2 Ethernet protocol for managing devices. LLDP allows an exchange of no; Default: no ) information between a PSE and a PD. Starting from RouterOS version 7.15, the setting has been replaced with the Neighbor Discovery `lldp-poe-power` property.
