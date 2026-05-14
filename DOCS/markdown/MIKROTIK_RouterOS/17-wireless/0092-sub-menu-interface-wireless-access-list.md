## Sub-menu: `/interface wireless access-list` 

Access list is used by access point to restrict allowed connections from other devices, and to control connection parameters. 

Access list rules are processed one by one until matching rule is found. Then the action in the matching rule is executed. If action specifies that client should be accepted, client is accepted, potentially overriding it's default connection parameters with ones specified in access list rule. 

There are the following parameters for access list rules: 

client matching parameters: 

address - MAC address of the client 

interface - optional interface to compare with the interface to which client actually connects to time - time of day and days when rule matches signal-range - range in which client signal must fit for the rule to match allow-signal-out-of-range - option which permits client's signal to be out of the range always or for some time interval connection parameters: 

ap-tx-limit - tx speed limit in direction to client client-tx-limit - tx speed limit in direction to AP (applies to RouterOS clients only) private-passphrase - PSK passphrase to use for this client if some PSK authentication algorithm is used vlan-mode - VLAN tagging mode specifies if traffic coming from client should get tagged (and untagged when going to client). vlan-id - VLAN ID to use if doing VLAN tagging 

Operation: 

Access list rules are checked sequentially. Disabled rules are always ignored. Only the first matching rule is applied. If there are no matching rules for the remote connection, then the default values from the wireless interface configuration are used. If remote device is matched by rule that has authentication =no value, the connection from that remote device is rejected. 

Warning: If there is no entry in ACL about client which connects to AP (wireless,debug wlan2: A0:0B:BA:D7:4D:B2 not in local ACL, by default accept), then ACL for this client is ignored during all connection time. 

For example, if client's signal during connection is -41 and we have ACL rule 

```
/interface/wireless/access-list
```

```
add authentication=yes forwarding=yes interface=wlan2 signal-range=-55..0
```

Then the connection is matched to the ACL rule, but if signal drops below -55, client will not be disconnected. 

Please note that if "default-authentication=yes" is set on the wireless interface, clients will be able to join even if there are no matching access-list entries. To make it work correctly it is required that client is matched by any of ACL rules. 

If we modify ACL rules in the previous example to: 

```
/interface/wireless/access-list
add interface=wlan2 signal-range=-55..0
add authentication=no forwarding=no interface=wlan2 signal-range=-120..-56
```

Then if signal drops to -56, client will be disconnected. 

1400
