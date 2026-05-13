## CAPsMAN Access-list 

Access list on CAPsMAN is an ordered list of rules that is used to allow/deny clients to connect to any CAP under CAPsMAN control. When a client attempts to connect to a CAP that is controlled by CAPsMAN, CAP forwards that request to CAPsMAN. As a part of the registration process, CAPsMAN consults an access list to determine if a client should be allowed to connect. The default behavior of the access list is to allow a connection. 

Access list rules are processed one by one until a matching rule is found. Then the action in the matching rule is executed. If action specifies that the client should be accepted, the client is accepted, potentially overriding its default connection parameters with ones specified in access-list rule. 

An access list is configured in the /caps-man access-list menu. There are the following parameters for access-list rules: 

client matching parameters: address - MAC address of the client mask - MAC address mask to apply when comparing client address interface - optional interface to compare with an interface to which client actually connects to time - a time of day and days when rule matches 

signal-range - range in which client signal must fit for a rule to match allow-signal-out-of-range - an option that permits the client's signal to be out of the range always or for some time interval action parameter - specifies an action to take when client matches: 

accept - accept client reject - reject client query-radius - query RADIUS server if a particular client is allowed to connect connection parameters: 

ap-tx-limit - tx speed limit in direction to client client-tx-limit - tx speed limit in direction to AP (applies to RouterOS clients only) client-to-client-forwarding - specifies whether to allow forwarding data received from this client to other clients connected to the same interface 

private-passphrase - PSK passphrase to use for this client if some PSK authentication algorithm is used radius-accounting - specifies if RADIUS traffic accounting should be used if RADIUS authentication gets done for this client vlan-mode - VLAN tagging mode specifies if traffic coming from a client should get tagged (and untagged when going to a client). vlan-id - VLAN ID to use if doing VLAN tagging.
