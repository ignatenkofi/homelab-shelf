## Session Establishment 

Lets look closely on how clients sessions gets authenticated and established over the LAC. 

**==> picture [24 x 24] intentionally omitted <==**

Client initiates PPPoE call 

LAC and Client begins LCP negotiation 

after CHAP has been negotiated, LAC sends CHAP challenge 

Client sends CHAP response 

LAC checks whether client session should be forwarded to the LNS based on received domain name. Check can be done locally or using RADIUS server. Client also can be authenticated here before forwarding session. 

- LAC brings up an L2TP tunnel 

LNS checks if the LAC is allowed to open a tunnel and run the authentication process. The Tunnel is up and ready to forward VPDN sessions. LAC forwards negotiated with the client LCP options, username and password to the LNS 

LNS authenticates the client locally or using RADIUS and sends CHAP response 

IP Control Protocol (IPCP) phase is performed, IP addresses and routes are installed. At this point sessions is considered established. 

1243
