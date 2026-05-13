## Discovery phase 

There are four steps to the Discovery stage. When it completes, both peers know the PPPoE SESSION_ID and the peer's Ethernet address, which together define the PPPoE session uniquely: 

1. PPPoE Active Discovery Initialization (PADI) - The PPPoE client sends out a PADI packet to the broadcast address. This packet can also populate the "service-name" field if a service name has been entered in the dial-up networking properties of the PPPoE client. If a service name has not been entered, this field is not populated 

2. PPPoE Active Discovery Offer (PADO) - The PPPoE server, or Access Concentrator, should respond to the PADI with a PADO if the Access Concentrator is able to service the "service-name" field that had been listed in the PADI packet. If no "service-name" field had been listed, the Access Concentrator will respond with a PADO packet that has the "service-name" field populated with the service names that the Access Concentrator can service. The PADO packet is sent to the unicast address of the PPPoE client 

3. PPPoE Active Discovery Request (PADR) - When a PADO packet is received, the PPPoE client responds with a PADR packet. This packet is sent to the unicast address of the Access Concentrator. The client may receive multiple PADO packets, but the client responds to the first valid PA 

1250 

   - DO that the client received. If the initial PADI packet had a blank "service-name" field filed, the client populates the "service-name" field of the PADR packet with the first service name that had been returned in the PADO packet. 

4. PPPoE Active Discovery Session Confirmation (PADS) - When the PADR is received, the Access Concentrator generates a unique session identification (ID) for the Point-to-Point Protocol (PPP) session and returns this ID to the PPPoE client in the PADS packet. This packet is sent to the unicast address of the client. 

PPPoE session termination: 

- PPPoE Active Discovery Terminate (PADT) - Can be sent anytime after a session is established to indicate that a PPPoE session terminated. It can be sent by either server or client.
