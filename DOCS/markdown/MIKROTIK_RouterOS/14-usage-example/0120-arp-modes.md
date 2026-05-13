## ARP Modes 

It is possible to set several ARP modes on the interface configuration. 

- `disabled` - the interface will not use ARP 

- `enabled` - the interface will use ARP 

- `local-proxy-arp` - the router performs proxy ARP on the interface and sends replies to the same interface 

- `proxy-arp` - the router performs proxy ARP on the interface and sends replies to other interfaces 

`reply-only` - the interface will only reply to requests originated from matching IP address/MAC address combinations which are entered as static entries in the IP/ARP table. No dynamic entries will be automatically stored in the IP/ARP table. Therefore for communications to be successful, a valid static entry must already exist.
