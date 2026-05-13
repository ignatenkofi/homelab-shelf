## Introduction 

Network Address Translation is an Internet standard that allows hosts on local area networks to use one set of IP addresses for internal communications and another set of IP addresses for external communications. A LAN that uses NAT is ascribed as a natted network. For NAT to function, there should be a NAT gateway in each natted network. The NAT gateway (NAT router) performs IP address rewriting on the way while packets travel from/to LAN. In RouterOS NAT is supported for IPv4. RouterOS does not support NAT64. 

Nat matches only the first packet of the connection, connection tracking remembers the action and performs on all other packets belonging to the same connection. 

**==> picture [13 x 13] intentionally omitted <==**

Whenever NAT rules are changed or added, the connection tracking table should be cleared otherwise NAT rules may seem to be not functioning correctly until the connection entry expires.
