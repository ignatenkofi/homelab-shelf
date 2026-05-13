## Types of NAT: 

**==> picture [504 x 186] intentionally omitted <==**

There are two types of NAT: 

source NAT or srcnat. This type of NAT is performed on packets that are originated from a natted network. A NAT router replaces the private source address of an IP packet with a new public IP address as it travels through the router. A reverse operation is applied to the reply packets traveling in the other direction. 

destination NAT or dstnat. This type of NAT is performed on packets that are destined for the natted network. It is most commonly used to make hosts on a private network to be accessible from the Internet. A NAT router performing dstnat replaces the destination IP address of an IP packet as it travels through the router toward a private network. 

Since RouterOS v7 the firewall NAT has two new INPUT and OUTPUT chains which are traversed for packets delivered to and sent from applications running on the local machine: 

647 

- input - used to process packets entering the router through one of the interfaces with the destination IP address which is one of the router's addresses. Packets passing through the router are not processed against the rules of the input chain. output - used to process packets that originated from the router and leave it through one of the interfaces. Packets passing through the router are not processed against the rules of the output chain.
