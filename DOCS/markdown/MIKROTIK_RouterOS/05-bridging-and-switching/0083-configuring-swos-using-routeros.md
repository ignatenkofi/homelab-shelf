## Configuring SwOS using RouterOS 

Since RouterOS 6.43 it is possible to load, save and reset SwOS configuration, as well as upgrade SwOS and set an IP address for the CRS3xx series switches by using RouterOS. 

Save configuration with `/system swos save-config` 

**==> picture [13 x 13] intentionally omitted <==**

The configuration will be saved on the same device with `swos.config` as a filename, make sure you download the file from your device since the configuration file will be removed after a reboot. 

Load configuration with `/system swos load-config` Change password with `/system swos password` Reset configuration with `/system swos reset-config` Upgrade SwOS from RouterOS using `/system swos upgrade` 

**==> picture [13 x 13] intentionally omitted <==**

The upgrade command will automatically install the latest available SwOS primary backup version, make sure that your device has access to the Internet in order for the upgrade process to work properly. When the device is booted into SwOS, the version number will include the letter "p", indicating a primary backup version. You can then install the latest available SwOS secondary main version from the SwOS "Upgrade" menu. 

**==> picture [13 x 13] intentionally omitted <==**

Starting from RouterOS version 7.17 device-mode restricts SwOS/RouterOS transition for dual-boot; in order to enable: system/device-mode /update routerboard=yes 

**==> picture [516 x 190] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address-acquisition-mode  (d Changes address acquisition method:<br>hcp-only | dhcp-with-fallback  dhcp-only - uses only a DHCP client to acquire address<br>| static; Default: dhcp-with-<br>fallback ) dhcp-with-fallback - for the first 10 seconds will try to acquire address using a DHCP client. If the request is<br>unsuccessful, then address falls back to static as defined by static-ip-address property<br>static - address is set as defined by static-ip-address property<br>allow-from  (IP/Mask; Default: IP address or a network from which the switch is accessible. By default, the switch is accessible by any IP address.<br>0.0.0.0/0 )<br>allow-from-ports  (name;  List of switch ports from which the device is accessible. By default, all ports are allowed to access the switch<br>Default: )<br>allow-from-vlan  (integer: 0.. VLAN ID from which the device is accessible. By default, all VLANs are allowed<br>4094; Default: 0 )<br>**----- End of picture text -----**<br>

409 

identity (name; Default: Mikr Name of the switch (used for Mikrotik Neighbor Discovery protocol) otik ) static-ip-address (IP; Default: IP address of the switch in case address-acquisition-mode is either set to dhcp-with-fallback or static. By setting a static 192.168.88.1 ) IP address, the address acquisition process does not change, which is DHCP with fallback by default. This means that the configured static IP address will become active only when there is going to be no DHCP servers in the same broadcast domain
