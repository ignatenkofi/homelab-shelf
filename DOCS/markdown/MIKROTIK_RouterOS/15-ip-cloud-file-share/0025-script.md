## Script 

It is possible to add a script that will be executed when a prefix or an address is acquired and applied or expires and is removed using the DHCP client. There are separated sets of variables that will have the value set by the client depending on prefix or address status change as the client can acquire both and each of them can have a different effect on the router configuration. 

Available variables for dhcp-client 

pd-valid - value - 1 or 0 - if prefix is acquired and it is applied or not 

pd-prefix - value ipv6/num (ipv6 prefix with mask) - the prefix inself 

- na-valid - value - 1 or 0 - if address is acquired and it is applied or not 

- na-address - value - ipv6 address - the address
