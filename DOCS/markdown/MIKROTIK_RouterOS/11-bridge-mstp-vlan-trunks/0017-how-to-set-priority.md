## How to set priority 

Priority of packets can be set using `action=set-priority` in IP firewall mangle rules or bridge filter/nat rules. Priority can be set to a specific value or taken from the ingress priority using the `from-ingress` setting. Ingress priority is the priority value that was detected on the incoming packet, if available. Currently, there are 2 sources of ingress priority - priority in the VLAN header and priority from the WMM packet received over a wireless interface. For all other packets ingress priority is 0. 

Note that ingress priority value is not automatically copied to IP mangle `priority` value, the correct rule needs to be set up to do this. 

There are 2 ways to control priority - assign priority with rules with particular matchers (protocol, addresses, etc.) or set it from ingress priority. Both options require setting up correct rules. 

625 

This essentially means that if it is not possible or wanted to classify packets by rules, the configuration of the network must be such that the router can extract ingress priority from incoming frames. Remember there are currently 2 sources for this - VLAN tag in packets and received WMM packets. 

**==> picture [13 x 13] intentionally omitted <==**

Do not mix the priority of queues with the priority assigned to packets. Priorities of queues work separately and specify the "importance" of the queue and have meaning only within a particular queue setup. Think of packet priority as some kind of mark, that gets attached to the packet by rules. Also, take into account that this mark currently is only used for outgoing packets when going over WMM enabled link, and in case VLAN tagged packet is sent out (no matter if that packet is tagged locally or bridged).
