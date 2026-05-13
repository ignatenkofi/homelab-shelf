## Sub-menu: `/ip neighbor` 

**==> picture [516 x 327] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP) The highest IP address configured on a discovered device<br>address6  (IPv6) IPv6 address configured on a discovered device<br>age  (time) Time interval since last discovery packet<br>discovered-by  (cdp|lldp|mndp) Shows the list of protocols the neighbor has been discovered by. The property is available since<br>RouterOS version 7.7.<br>board  (string) RouterBoard model. Displayed only to devices with installed RouterOS<br>identity  (string) Configured system identity<br>interface  (string) Interface name to which discovered device is connected<br>interface-name  (string) Interface name on the neighbor device connected to the L2 broadcast domain. Applies to CDP.<br>ipv6  (yes | no) Shows whether the device has IPv6 enabled.<br>mac-address  (MAC) Mac address of the remote device. Can be used to connect with mac-telnet.<br>platform  (string) Name of the platform. For example "MikroTik", "cisco", etc.<br>software-id  (string) RouterOS software ID on a remote device. Applies only to devices installed with RouterOS.<br>system-caps  (string) System capabilities reported by the Link-Layer Discovery Protocol (LLDP).<br>system-caps-enabled  (string) Enabled system capabilities reported by the Link-Layer Discovery Protocol (LLDP).<br>unpack  (none|simple|uncompressed- Shows the discovery packet compression type.<br>headers|uncompressed-all)<br>**----- End of picture text -----**<br>


1148 

**==> picture [516 x 58] intentionally omitted <==**

**----- Start of picture text -----**<br>
uptime  (time) Uptime of remote device. Shown only to devices installed with RouterOS.<br>version  (string) Version number of installed software on a remote device<br>running  (string array) Report a list of "features" running on neighbour device. Currently lists only "CAPsMAN" feature.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Starting from RouterOS v6.45, the number of neighbor entries are limited to (total RAM in megabytes)*16 per interface to avoid memory exhaustion.
