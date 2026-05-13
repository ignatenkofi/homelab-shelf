## Dynamic switch rule configuration 

In some network configurations, additional access rules are needed for a particular supplicant to restrict or allow certain network services. This can be done using a Mikrotik-Switching-Filter attribute, please see the RADIUS vendor dictionary. When a client is successfully authenticated by an authentication server, the server can pass back the Mikrotik-Switching-Filter attribute. Based on the received information, the authenticator will create dynamic access rules on a switch port where the client resides. These rules will be active as long as the client session is active and the interface is running. There are certain order and restrictions regarding correct switch rule implementation: 

- The `mac-protocol` , `src-mac-address` (available only since RouterOS 7.2 version), `src-address` (IPv4/mask, available only since RouterOS 7.2 version), `dst-address` (IPv4/mask), `protocol` (IPv4) `src-port` (L4, available only since RouterOS 7.2 version), `dst-port` (L4) conditional parameters are supported Hexadecimal or decimal representation can be used for `mac-protocol` and `protocol` parameters (e.g. `protocol 17` or `protocol 0x11` ) The `src-port` and `dst-port` support single or range values (e.g. `src-port 10` or `src-port 10-20` ) The `src-mac-address` support "xx:xx:xx:xx:xx:xx" or "xxxxxxxxxxxx" formats, and switch rule without any source MAC address can be set with "none" keyword (e.g. `src-mac-address none` ) The `src-mac-address` (if not already set by the attribute) `, switch` and `ports` conditional parametrs are automatically set for each rule Each rule should end with an action property, supported values are either drop or allow . If no action property is set, the default allow value will be used. 

- Multiple rules are supported for a single supplicant and they must be separated by a comma "," 

288 

Below are some examples of Mikrotik-Switching-Filter attributes and dynamic switch rules they create: 

```
# Drop ARP frames (EtherType: 0x0806 or 2054)
Mikrotik-Switching-Filter = "mac-protocol 2054 action drop"
```

```
/interface ethernet switch rule print
Flags: X - disabled, I - invalid, D - dynamic
 0  D ;;; dot1x dynamic
```

```
      switch=switch1 ports=ether1 src-mac-address=CC:2D:E0:11:22:33/FF:FF:FF:FF:FF:FF mac-protocol=arp copy-
to-cpu=no redirect-to-cpu=no mirror=no new-dst-ports=""
```

```
# Allow UDP (IP protocol: 0x11 or 17) destination port 100 and drop all other packets
Mikrotik-Switching-Filter = "protocol 17 dst-port 100 action allow, action drop"
```

```
/interface ethernet switch rule print
Flags: X - disabled, I - invalid, D - dynamic
 0  D ;;; dot1x dynamic
      switch=switch1 ports=ether1 src-mac-address=CC:2D:E0:11:22:33/FF:FF:FF:FF:FF:FF protocol=udp dst-
port=100 copy-to-cpu=no redirect-to-cpu=no mirror=no
```

```
 1  D ;;; dot1x dynamic
```

```
      switch=switch1 ports=ether1 src-mac-address=CC:2D:E0:11:22:33/FF:FF:FF:FF:FF:FF copy-to-cpu=no
redirect-to-cpu=no mirror=no new-dst-ports=""
```

```
# Allow only authenticated source MAC address, drop all other packets
Mikrotik-Switching-Filter = "action allow, src-mac-address none action drop"
```

```
/interface ethernet switch rule print
Flags: X - disabled, I - invalid; D - dynamic
 0  D ;;; dot1x dynamic
```

```
      switch=switch1 ports=ether1 src-mac-address=CC:2D:E0:01:6D:EB/FF:FF:FF:FF:FF:FF copy-to-cpu=no
redirect-to-cpu=no mirror=no
```

```
 1  D ;;; dot1x dynamic
```

```
      switch=switch1 ports=ether1 copy-to-cpu=no redirect-to-cpu=no mirror=no new-dst-ports=""
```

In our example, Supplicant2 on ether2 is only allowed to access the 192.168.50.0/24 network with UDP destination port 50, all other traffic should be dropped. First, make sure that hardware offloading is working on bridge ports, otherwise switch rules might not work properly. 

```
/interface bridge port print
```

```
Flags: X - disabled, I - inactive, D - dynamic, H - hw-offload
```

```
 #     INTERFACE                   BRIDGE                   HW  PVID PRIORITY  PATH-COST INTERNAL-PATH-
COST    HORIZON
 0   H ether1                      bridge1                  yes    1     0x80         10
10       none
 1   H ether2                      bridge1                  yes    1     0x80         10
10       none
 2   H ether12                     bridge1                  yes    1     0x80         10
10       none
```

With enabled RADIUS debug logs it is possible to see complete RADIUS message packets with all attributes. In our example, Mikrotik-Switching-Filter attribute is received in Access-Accept message from Radius server: 

```
02:35:38 radius,debug,packet received Access-Accept with id 121 from 10.1.2.3:1812
```

```
(..)
```

```
02:35:38 radius,debug,packet     MT-Switching-Filter = "mac-protocol 2048 dst-address 192.168.50.0/24 dst-
port 50 protocol 17 action allow,action drop"
```

The dynamic switch rules are now present under the switch menu: 

289 

```
/interface ethernet switch rule print
```

```
Flags: X - disabled, I - invalid, D - dynamic
 0  D ;;; dot1x dynamic
```

```
      switch=switch1 ports=ether2 src-mac-address=CC:2D:E0:11:22:33/FF:FF:FF:FF:FF:FF mac-protocol=ip dst-
address=192.168.50.0/24 protocol=udp dst-port=50 copy-to-cpu=no redirect-to-cpu=no mirror=no
```

```
 1  D ;;; dot1x dynamic
```

```
      switch=switch1 ports=ether2 src-mac-address=CC:2D:E0:11:22:33/FF:FF:FF:FF:FF:FF copy-to-cpu=no
redirect-to-cpu=no mirror=no new-dst-ports=""
```

**==> picture [13 x 13] intentionally omitted <==**

Dynamic switch rules will only apply to RouterBoards with switch rule support - CRS3xx, CRS5xx series switches, CCR2116, CCR2216, and devices with QCA8337, Atheros8327 and Atheros8316 switch chips. CRS1xx/2xx series switches do no support this functionality. Take into consideration the maximum number of rules for each device, see CRS3xx, CRS5xx, CCR2116, CCR2216 table and basic switch chip table
