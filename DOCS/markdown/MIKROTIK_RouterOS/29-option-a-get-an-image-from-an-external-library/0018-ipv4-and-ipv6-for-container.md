## IPv4 and IPv6 for Container 

In this networking setup your Container will be able to communicate over IPv4 and IPv6. The solution is based on Bridge with NAT networking setup. 

The network configuration: 

```
/ip address
add address=172.17.0.1/24 interface=containers
/ip firewall nat
add action=masquerade chain=srcnat src-address=172.17.0.0/24
add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=80 protocol=tcp to-addresses=172.
17.0.2 to-ports=80
/ipv6 address
add address=fd8d:5ad2:24:2::1 interface=containers
/ipv6 firewall nat
add action=masquerade chain=srcnat src-address=fd8d:5ad2:24:2::/64
add action=dst-nat chain=dstnat dst-address=0:0:0:0:0:ffff:c0a8:5801 dst-port=80 protocol=udp to-
address=fd8d:5ad2:24:2::2 to-ports=80
/interface veth
add address=172.17.0.2/24,fd8d:5ad2:24:2::2/64 gateway=172.17.0.1 gateway6=fd8d:5ad2:24:2::1 name=veth1
/interface/bridge/port add bridge=containers interface=veth1
```

The webapp Container configuration: 

```
/container/add remote-image=nginx interface=veth1 root-dir=disk1/images/nginx name=nginx start-on-
boot=yes logging=yes
```
