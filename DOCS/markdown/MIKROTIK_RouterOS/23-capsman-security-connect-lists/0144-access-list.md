## Access List 

Access list on CAPsMAN is an ordered list of rules that is used to allow/deny clients to connect to any CAP under CAPsMAN control. When client attempts to connect to a CAP that is controlled by CAPsMAN, CAP forwards that request to CAPsMAN. As a part of registration process, CAPsMAN consults access list to determine if client should be allowed to connect. The default behaviour of the access list is to allow connection. 

Access list rules are processed one by one until matching rule is found. Then the action in the matching rule is executed. If action specifies that client should be accepted, client is accepted, potentially overriding it's default connection parameters with ones specified in access list rule. 

1486 

Access list is configured in /caps-man access-list menu. There are the following parameters for access list rules: 

client matching parameters: 

address - MAC address of client (or, if mask is specified, only those parts will be checked as per the mask, so to match vendor D8 from "D8:1C:79:6E:1E:FE", simply enter a bogus entry, such as "D8:00:00:00:00" and then use the mask as per next line) 

mask - MAC address mask to apply when comparing client address. For example, use FF:00:00:00:00:00 to match only the first octet of the specified MAC address. In above example, regardless of entered MAC, it will match only first octet. Similarly, entering 00:00:00:00: FF will only match the last octet (FE) of a hypotetical MAC "D8:1C:79:6E:1E:FE"). So in the mac line, you could just enter 00:00:00:00:00: FE, if you would use such a mask. 

interface - optional interface to compare with interface to which client actually connects to 

- time - time of day and days when rule matches 

signal-range - range in which client signal must fit for rule to match 

action parameter - specifies action to take when client matches: 

accept - accept client 

reject - reject client 

query-radius - query RADIUS server if particular client is allowed to connect 

connection parameters: 

ap-tx-limit - tx speed limit in direction to client 

client-tx-limit - tx speed limit in direction to AP (applies to RouterOS clients only) 

- client-to-client-forwarding - specifies whether to allow forwarding data received from this client to other clients connected to the same interface 

private-passphrase - PSK passphrase to use for this client if some PSK authentication algorithm is used 

radius-accounting - specifies if RADIUS traffic accounting should be used if RADIUS authentication gets done for this client vlan-mode - VLAN tagging mode specifies if traffic coming from client should get tagged (and untagged when going to client). vlan-id - VLAN ID to use if doing VLAN tagging.
