## BGP Basics 

BGP routers exchange reachability information by means of a transport protocol, which in the case of BGP is TCP (port 179). Upon forming a TCP connection these routers exchange OPEN messages to negotiate and confirm supported capabilities. 

After agreeing on capabilities to use, the session is considered to be established and peers can start to exchange NLRIs via UPDATE messages. This information contains an indication of what sequence of full paths (BGP AS numbers) the route should take in order to reach the destination network (NLRI prefix). 

The peers initially exchange their full routing tables and after the initial exchange, incremental updates are sent as the routing tables change. Thus, BGP does not require a periodic refresh of the entire BGP routing table. 

BGP maintains the routing table version number which must be the same between any two given peers for the duration of the connection. 

KEEPALIVE messages are sent periodically to ensure that the connection is up and running, if KEEPALIVE messages are not received within the Hold Time interval, the connection will be closed. 

To respond to errors or special conditions, NOTIFICATION messages can be generated and sent to the remote peer, notification message type also indicates whether the connection should be immediately closed. 

There can be two types of BGP connections: 

iBGP - is an "internal" link connecting peers from the same AS 

eBGP - is an "external" link connecting peers belonging to two different AS-es 

A particular AS might have multiple BGP speakers and provide transit service to other AS-es. This implies that BGP speakers must maintain a consistent view of routing within the AS.  A consistent view of the routes exterior to the AS is provided by having all BGP routers within the AS establish direct iBGP connections with each other (full mesh) or by utilizing a Router Reflector setup. 

Using a set of administrative policies BGP speakers within the AS come to an agreement as to which entry/exit point to use for a particular destination. This information is communicated to the interior routers of the AS using the interior routing protocol (IGP), for example, OSPF, RIP, or static routing. In certain setups, iBGP can take the IGP protocol role as well. 

For certain BGP attributes handling behavior may change depending on what type of connection is set up, for example, the LOCAL-PREF attribute is not advertised to eBGP peers. 

RouterOS divides configuration and session monitoring into four menus: 

instance menu ( `/routing/bgp/instance` ) 

connection menu ( `/routing/bgp/connection` ) sessions menu( `/routing/bgp/session` ) template menu ( `/routing/bgp/template` )
