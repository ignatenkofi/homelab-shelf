## Recommended Local Network and Internet Gateway Configuration 

These ZeroTier recommended guidelines are consistent with the vast majority of typical deployments using commodity gateways and access points: 

Don't restrict outbound UDP traffic. 

Supporting either UPnP or NAT-PMP on your network can greatly improve performance by allowing ZeroTier endpoints to map external ports and avoid NAT traversal entirely. 

1284 

- IPv6 is recommended and can greatly improve direct connection reliability if supported on both ends of a direct link. If present it should be implemented without NAT (NAT is wholly unnecessary with IPv6 and only adds complexity) and with a stateful firewall that permits bidirectional UDP conversations. 

- Don't use "symmetric" NAT. Use "full cone" or "port restricted cone" NAT. Symmetric NAT is extremely hostile to peer-to-peer traffic and will degrade VoIP, video chat, games, WebRTC, and many other protocols as well as ZeroTier. 

- No more than one layer of NAT should be present between ZeroTier endpoints and the Internet. Multiple layers of NAT introduce connection instability due to chaotic interactions between states and behaviors at different levels. No Double NAT. 

NATs should have a port mapping or connection timeout no shorter than 60 seconds. 

- Place no more than about 16,000 devices behind each NAT-managed external IP address to ensure that each device can map a sufficient number of ports. 

Switches and wireless access points should allow direct local traffic between local devices. Turn off any "local isolation" features. Some switches might allow finer-grained control, and on these, it would be sufficient to allow local UDP traffic to/from 9993 (or in general).
