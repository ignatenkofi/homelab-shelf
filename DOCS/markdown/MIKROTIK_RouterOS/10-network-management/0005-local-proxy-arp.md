## Local Proxy Arp 

If the ARP property is set to `local-proxy-arp` on an interface, then the router performs proxy ARP to/from this interface only. i.e. for traffic that comes in and goes out of the same interface. In a normal LAN, the default behavior is for two network hosts to communicate directly with each other, without involving the router. 

With `local-proxy-arp` enabled, the router will respond to all client hosts with the router's own interface MAC address instead of the other host's MAC address. 

E.g. If Host A (192.168.88.2/24) queries for the MAC address of Host B (192.168.88.3/24), the router would respond with its own MAC address. In other words, if `local-proxy-arp` is enabled, the router would assume responsibility for forwarding traffic between Host A 192.168.88.2 and Host B 192.168.88.3. All the ARP cache entries on Hosts A and B will reference the router's MAC address. In this case, the router is performing `local-proxyarp` for the entire subnet 192.168.88.0/24. 

An example for RouterOS `local-proxy-arp` could be a bridge setup with a DHCP server and isolated bridge ports where hosts from the same subnet can reach each other only at Layer3 through bridge IP. 

```
/interface bridge
add arp=local-proxy-arp name=bridge1
/interface bridge port
add bridge=bridge1 horizon=1 interface=ether2
add bridge=bridge1 horizon=1 interface=ether3
add bridge=bridge1 horizon=1 interface=ether4
```
