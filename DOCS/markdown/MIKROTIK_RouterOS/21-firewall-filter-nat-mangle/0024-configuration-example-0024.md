## Configuration example 

**==> picture [504 x 334] intentionally omitted <==**

By default, ZeroTier is designed to be zero-configuration. A user can start a new ZeroTier node without having to write configuration files or provide the IP addresses of other nodes. It’s also designed to be fast. Any two devices in the world should be able to locate each other and communicate almost instantly so the following example will enable ZeroTier on RouterOS device and connect one mobile phone using the ZeroTier application. 

1.  Register on my.zerotier.com and Create A Network , obtain the Network ID, in this example: 1d71939404912b40; 

**==> picture [361 x 104] intentionally omitted <==**

1285 

2.  Download and Install ZeroTier NPK package in RouterOS, you can find under in the "Extra packages", upload package on the device and reboot the unit; 

3.  Enable the default (official) ZeroTier instance: 

```
[admin@mikrotik] > zerotier/enable zt1
```

4.  Add a new network, specifying the network ID you created in the ZeroTier cloud console: 

```
[admin@mikrotik] zerotier/interface/add network=1d71939404912b40 instance=zt1
```

5.  Verify ZeroTier configuration: 

```
[admin@MikroTik] > zerotier/interface/print
Flags: R - RUNNING
Columns: NAME, MAC-ADDRESS, NETWORK, NETWORK-NAME, STATUS
#   NAME       MAC-ADDRESS        NETWORK           NETWORK-NAME     STATUS
0 R zerotier1  42:AC:0D:0F:C6:F6  1d71939404912b40  modest_metcalfe  OK
```

6.  Now you might need to allow connections from the ZeroTier interface to your router, and optionally , to your other LAN interfaces: 

```
/ip firewall filter add action=accept chain=forward in-interface=zerotier1 place-before=0
/ip firewall filter add action=accept chain=input in-interface=zerotier1 place-before=0
```

7.  Install a ZeroTier client on your smartphone or computer, follow the ZeroTier manual on how to connect to the same network from there. 8.  If "Access Control" is set to "Private" , you must authorize nodes before they become members: 

**==> picture [361 x 122] intentionally omitted <==**

9. `[admin@MikroTik] > ip/address/print where interface~"zero" Flags: D - DYNAMIC Columns: ADDRESS, NETWORK, INTERFACE #   ADDRESS             NETWORK        INTERFACE 3 D 192.168.192.105/24  192.168.192.0  zerotier1` 

```
[admin@MikroTik] > ping 192.168.192.252 count=3
SEQ HOST                                     SIZE TTL TIME
STATUS
0 192.168.192.252                            56  64 407us
1 192.168.192.252                            56  64 452us
2 192.168.192.252                            56  64 451us
sent=3 received=3 packet-loss=0% min-rtt=407us avg-rtt=436us max-rtt=452us
```

**==> picture [13 x 13] intentionally omitted <==**

You should specify routes to specific internal subnets in the ZeroTier cloud console, to make sure you can access those networks when connecting from other devices.
