## Passthrough Example 

Some LTE interfaces support the LTE Passthrough feature where the IP configuration is applied directly to the client device. In this case, modem firmware is responsible for the IP configuration, and the router is used only to configure modem settings - APN, Network Technologies, and IP-Type. In this configuration, the router will not get IP configuration from the modem. The LTE Passthrough modem can pass both IPv4 and IPv6 addresses if that is supported by the modem. Some modems support multiple APNs where you can pass the traffic from each APN to a specific router interface. 

Passthrough will only work for one host. The router will automatically detect the MAC address of the first received packet and use it for the Passthrough. If there are multiple hosts on the network it is possible to lock the Passthrough to a specific MAC. On the host on the network where the Passthrough is providing the IP a DHCP-Client should be enabled on that interface too. Note, that it will not be possible to connect to the LTE router via a public lte IP address or from the host which is used by the passthrough. It is suggested to create an additional connection from the LTE router to the host for configuration purposes. For example vlan interface between the LTE router and host. 

To enable the Passthrough a new entry is required or the default entry should be changed in the ' `/interface lte apn` ' menu 

**==> picture [13 x 13] intentionally omitted <==**

Passthrough is not supported by all chipsets. to check if your modem supports passthrough: 

```
/interface/lte/show-capabilities [find]
```

Examples. 

To configure the Passthrough on ether1: 

```
[admin@MikroTik] > /interface lte apn add apn=apn1 passthrough-interface=ether1
[admin@MikroTik] > /interface lte set lte1 apn-profiles=apn1
```

To configure the Passthrough on ether1 host 00:0C:42:03:06:AB: 

817 

```
[admin@MikroTik] > /interface lte apn add apn=apn1 passthrough-interface=ether1 passthrough-mac=00:0C:42:03:06:
AB
```

```
[admin@MikroTik] > /interface lte set lte1 apn-profiles=apn1
```

To configure multiple APNs on ether1 and ether2: 

```
[admin@MikroTik] > /interface lte apn add apn=apn1 passthrough-interface=ether1
[admin@MikroTik] > /interface lte apn add apn=apn2 passthrough-interface=ether2
[admin@MikroTik] > /interface lte set lte1 apn-profiles=apn1,apn2
```

To configure multiple APNs with the same APN for different interfaces: 

```
[admin@MikroTik] > /interface lte apn add name=interface1 apn=apn1
[admin@MikroTik] > /interface lte apn add name=interface2 apn=apn1 passthrough-interface=ether1
[admin@MikroTik] > /interface lte set lte1 apn-profiles=interface1
[admin@MikroTik] > /interface lte set lte2 apn-profiles=interface2
```

Additionally, you can override the default dynamic dhcp server parameters/options by creating a DHCP server manually on the same passthroughinterface. For example, the default lease-time is 1 minute: 

```
[admin@MikroTik] > ip dhcp-server/print detail
Flags: D - dynamic; X - disabled, I - invalid
```

```
 0 D  name="apn2" interface=ether2 lease-time=1m address-pool=static-only use-radius=no lease-script="" address-
lists=""
```

Now if you want to change the lease-time to for example 30 minutes, then you can create a new dhcp-server on the passthrough-interface, in this case, ether2: 

```
[admin@MikroTik] > /ip dhcp-server add interface=ether2 name=dhcp1 lease-time=30m
[admin@MikroTik] > ip dhcp-server/print detail
Flags: D - dynamic; X - disabled, I - invalid
```

```
 0    name="dhcp1" interface=ether2 lease-time=30m address-pool=static-only use-radius=no lease-script=""
address-lists=""
```
