## Session phase 

When the discovery stage is completed, both peers know PPPoE Session ID and other peer's Ethernet (MAC) address which together defines the PPPoE session. PPP frames are encapsulated in PPPoE session frames, which have Ethernet frame type 0x8864 . When a server sends confirmation and a client receives it, PPP Session is started that consists of the following stages: 

1. LCP negotiation stage 2. Authentication (CHAP/PAP) stage 3. IPCP negotiation stage - where the client is assigned an IP address. 

**==> picture [13 x 13] intentionally omitted <==**

If any process fails, the LCP negotiation establishment phase is started again. 

PPPoE server sends Echo-Request packets to the client to determine the state of the session, otherwise, the server will not be able to determine that session is terminated in cases when a client terminates session without sending Terminate-Request packet.
