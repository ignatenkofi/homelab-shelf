## RADIUS EAP pass-through authentication 

When using WPA EAP authentication type, clients that have passed MAC authentication are required to perform EAP authentication before being authorized to pass data on wireless network. With pass-through EAP method the access point will relay authentication to RADIUS server, and use following attributes in the Access-Request RADIUS message: 

- User-Name - EAP supplicant identity. This value is configured in the supplicant-identity property of the client security profile. Nas-Port-Id - name of wireless interface. 

- Calling-Station-Id - Client MAC address, encoded as "XX-XX-XX-XX-XX-XX". 

- Called-Station-Id - MAC address and SSID of the access point, encoded as "XX-XX-XX-XX-XX-XX:SSID" (pairs of MAC address digits separated by minus sign, followed by colon, followed by SSID value). 

- Acct-Session-Id - Added when radius-eap-accounting =yes. 

- Acct-Multi-Session-Id - MAC address of access point and client, and unique 8 byte value, that is shared for all accounting sessions that share single EAP authentication. Encoded as AA-AA-AA-AA-AA-AA-CC-CC-CC-CC-CC-CC-XX-XX-XX-XX-XX-XX-XX-XX. Added when radius-eapaccounting=yes. 

Access point uses following RADIUS attributes from the Access-Accept server response: 

Class - If present, value of this attribute is saved and included in Accounting-Request messages. 

Session-Timeout - Time, after which client will be disconnected. Additionally, access point will remember authentication result, and if during this time client reconnects, it will be authorized immediately, without repeating EAP authentication. 

Acct-Interim-Interval - Overrides value of interim-update .
