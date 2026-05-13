## MAC address authentication 

Implemented through the query-radius action, MAC address authentication is a way to implement a centralized whitelist of client MAC addresses using a RADIUS server. 

When a client device tries to associate with an AP, which is configured to perform MAC address authentication, the AP will send an access-request message to a RADIUS server with the device's MAC address as the user name and an empty password. If the RADIUS server answers with accessaccept to such a request, the AP proceeds with whatever regular authentication procedure (passphrase or EAP authentication) is configured for the interface.
