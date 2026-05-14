## `/zerotier/controller/` 

Every ZeroTier instance has a self-hosting network controller that can be used to host virtual networks. A controller is responsible for admitting members to the network, and issuing default configuration information including certificates. Controllers can in theory host up to 2^24 networks and serve many millions of devices (or more), but we recommend spreading large numbers of networks across many controllers for load balancing and fault tolerance reasons.
