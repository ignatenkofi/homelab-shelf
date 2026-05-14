## Switch Rules (ACL) 

Access Control List contains ingress policy and egress policy engines. See this table on how many rules each device supports. It is an advanced tool for wire-speed packet filtering, forwarding and modifying based on Layer2, Layer3 and Layer4 protocol header field conditions. 

ACL rules are checked for each received packet until a match has been found. If there are multiple rules that can match, then only the first rule will be triggered. A rule without any action parameters is a rule to accept the packet. 

Enabling features such as IGMP snooping, DHCP snooping, RoMON, PTP, or loop-protect can automatically create dynamic ACL rules. These rules should be considered when adding new ACL entries. Use the `place-before` property when creating a new rule, or the `move` command to adjust the ACL rule order. 

**==> picture [13 x 13] intentionally omitted <==**

It is not required to set `mac-protocol` to certain IP version when using L3 or L4 matchers, however, it is recommended to set the `macprotocol=ip` or `mac-protocol=ipv6` when filtering any IP packets. 

**==> picture [13 x 13] intentionally omitted <==**

When switch ACL rules are modified (e.g. added, removed, disabled, enabled, or moved), the existing switch rules will be inactive for a short time. This can cause some packet leakage during the ACL rule modifications.
