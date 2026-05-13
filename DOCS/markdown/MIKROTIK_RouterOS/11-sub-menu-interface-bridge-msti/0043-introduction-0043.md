## Introduction 

Firewall filters are used to allow or block specific packets forwarded to your local network, originating from your router, or destined to the router. 

There are two methods on how to set up filtering: 

allow specific traffic and drop everything else drop only malicious traffic, everything else is allowed. 

Both methods have pros and cons, for example, from a security point of view first method is much more secure, but requires administrator input whenever traffic for a new service needs to be accepted. This strategy provides good control over the traffic and reduces the possibility of a breach because of service misconfiguration. 

On the other hand, when securing a customer network it would be an administrative nightmare to accept all possible services that users may use. Therefore careful planning of the firewall is essential in advanced setups. 

A firewall filter consists of three predefined chains that cannot be deleted: 

**==> picture [504 x 173] intentionally omitted <==**

input - used to process packets entering the router through one of the interfaces with the destination IP address which is one of the router's addresses. Packets passing through the router are not processed against the rules of the input chain forward - used to process packets passing through the router output - used to process packets originating from the router and leaving it through one of the interfaces. Packets passing through the router are not processed against the rules of the output chain 

Firewall filter configuration is accessible from `ip/firewall/filter` menu for IPv4 and `ipv6/firewall/filter` menu for IPv6.
