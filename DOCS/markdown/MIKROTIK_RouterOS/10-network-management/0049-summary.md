## Summary 

The DHCP (Dynamic Host Configuration Protocol) is used for the easy distribution of IP addresses in a network. The MikroTik RouterOS implementation includes both server and client parts and is compliant with RFC 2131. 

The router supports an individual server for each Ethernet-like interface. The MikroTik RouterOS DHCP server supports the basic functions of giving each requesting client an IP address/netmask lease, default gateway, domain name, DNS-server(s) and WINS-server(s) (for Windows clients) information (set up in the DHCP networks submenu) 

In order for the DHCP server to work, IP pools must also be configured (do not include the DHCP server's own IP address into the pool range) and the DHCP networks. 

It is also possible to hand out leases for DHCP clients using the RADIUS server; the supported parameters for a RADIUS server are as follows: 

Access-Request: 

- NAS-Identifier - router identity 

- NAS-IP-Address - IP address of the router itself 

- NAS-Port - the ID of the interface where the DHCP server is configured. This value is the same as the IF-MIB::ifIndex NAS-Port-Id - the name of the interface where the DHCP server is configured NAS-Port-Type - Ethernet 

- Calling-Station-Id - client identifier (active-client-id) 

- Framed-IP-Address - IP address of the client (active-address) 

- Called-Station-Id - the name of DHCP server 

- User-Name - MAC address of the client (active-mac-address) 

- Password - " " 

Access-Accept: 

- Framed-IP-Address - IP address that will be assigned to a client 

- Framed-Pool - IP pool from which to assign an IP address to a client 

- Rate-Limit - Datarate limitation for DHCP clients. Format is: rx-rate[/tx-rate] [rx-burst-rate[/tx-burst-rate] [rx-burst-threshold[/tx-burst-threshold] [rxburst-time[/tx-burst-time][priority] [rx-rate-min[/tx-rate-min]]]]. All rates should be numbers with optional 'k' (1,000s) or 'M' (1,000,000s). If tx-rate is not specified, rx-rate is as tx-rate too. Same goes for tx-burst-rate and tx-burst-threshold and tx-burst-time. If both rx-burst-threshold and tx-burstthreshold are not specified (but burst-rate is specified), rx-rate and tx-rate are used as burst thresholds. If both rx-burst-time and tx-burst-time are not specified, 1s is used as default. Priority takes values 1..8, where 1 implies the highest priority, but 8 - the lowest. If rx-rate-min and tx-rate-min are not specified rx-rate and tx-rate values are used. The rx-rate-min and tx-rate-min values can not exceed rx-rate and tx-rate values. Ascend-Data-Rate - TX/RX data rate limitation if multiple attributes are provided, first limits tx data rate, second - RX data rate. If used together with Ascend-Xmit-Rate, specifies RX rate. 0 if unlimited 

- Ascend-Xmit-Rate - tx data rate limitation. It may be used to specify the TX limit only instead of sending two sequential Ascend-Data-Rate attributes (in that case Ascend-Data-Rate will specify the receive rate). 0 if unlimited Session-Timeout - max lease time (lease-time) 

**==> picture [13 x 13] intentionally omitted <==**

DHCP server requires a real interface to receive raw ethernet packets. If the interface is a Bridge interface, then the Bridge must have a real interface attached as a port to that bridge which will receive the raw ethernet packets. It cannot function correctly on a dummy (empty bridge) interface.
