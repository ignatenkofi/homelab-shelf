## Protect the Clients 

Before the actual set of rules, let's create a necessary `address-list` that contains all IPv4/6 addresses that cannot be forwarded. 

Notice that in this list multicast address range is added. It is there because in most cases multicast is not used. If you intend to use multicast forwarding, then this address list entry should be disabled.
