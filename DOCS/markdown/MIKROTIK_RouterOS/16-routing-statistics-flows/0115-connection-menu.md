## Connection Menu 

Let's look at a very basic eBGP configuration example assuming, that Router1 IP is 192.168.1.1, AS 65531 and Router2 IP 192.168.1.2, AS 65532: 

```
#Router1
/routing/bgp/instance
add name=i1 as=65531
```

```
/routing/bgp/connection
add name=toR2 remote.address=192.168.1.2 instance=i1 local.role=ebgp
```

1011 

```
#Router2
/routing/bgp/instance
add name=i1 as=65532
/routing/bgp/connection
add name=toR1 remote.address=192.168.1.1 instance=i1 local.role=ebgp
```

The BGP connection menu defines BGP outgoing connections as well as acts as a template matcher for incoming BGP connections. 

`local.role` parameter is used to indicate that this connection will be the eBGP. Also, notice that the connection does not require a remote AS number to be specified, RouterOS can determine a remote AS number dynamically from the first received OPEN message. 

The parameter equivalent to other vendors and older RouterOS "update-source" is " `local.address` ". In most cases, it can be left unconfigured, and let the router determine the address. 

When a local address is not specified, BGP will try to guess the local address depending on the current setup: 

if the peer is iBGP if loopback available pick the highest loopback address if loopback is not available pick any highest IP address on the router if the peer is eBGP if a remote peer's IP is not from a directly connected network: and multihop is not set, then throw an error and multihop is enabled: if loopback available pick the highest loopback address if loopback is not available pick any highest IP address on the router if a remote peer's IP is from a directly connected network: and multihop is not set: pick the local routers IP address from that connected network and multihop is set: if loopback available pick the highest loopback address if loopback is not available pick any highest IP address on the router 

In addition to connection-specific parameters, template-specific parameters are also directly exposed in this menu, for easier configuration in simple scenarios (when templates are not necessary). 

**==> picture [13 x 13] intentionally omitted <==**

Listening on subnets should not be enabled in unsafe environments, denial of service is possible with such configuration. Firewall must be configured to protect the router. See "listen" parameter for more details.
