## Access-Request packet 

Service-Type - always is "Framed" (only for PPPs) Framed-Protocol - always is "PPP" (only for PPPs) NAS-Identifier - router's identity name 

316 

- NAS-IP-Address - IP address of the router itself 

- NAS-Port - this Attribute indicates the physical port number of the NAS which is authenticating the user. Acct-Session-Id - unique session ID. The first two symbols of session ID represent service (PPP, Hotspot, etc.). The next symbol is incremented on each reboot. The last group of symbols is incremented on each new session. This means, that you can not get the same ID for 1 million reconnects on the same boot for the same RADIUS type service. If you lose session stop message and RADIUS server does still keep the session open, but then receives another session start message, then it must be aware that stop message was lost, close old session and start a new session. 

- NAS-Port-Type - async PPP - "Async"; PPTP and L2TP - "Virtual"; PPPoE - "Ethernet"; ISDN - "ISDN Sync"; HotSpot - "Ethernet | Cable | Wireless-802.11" (according to the value of nas-port-type parameter in /ip hotspot profile) 

- Calling-Station-Id - PPPoE and HotSpot- client MAC address in capital letters; PPTP and L2TP - client public IP address 

- Called-Station-Id - PPPoE - service name; PPTP and L2TP - server IP address; HotSpot - name of the HotSpot server 

- NAS-Port-Id - async PPP - serial port name; PPPoE - ethernet interface name on which server is running; HotSpot - name of the physical HotSpot interface (if bridged, the bridge port name is showed here); not present for ISDN, PPTP and L2TP 

- Framed-IP-Address - IP address of HotSpot client after Universal Client translation 

- Mikrotik-Host-IP - IP address of HotSpot client before Universal Client translation (the original IP address of the client) 

- User-Name - client login name 

- MS-CHAP-Domain - User domain, if present 

- Mikrotik-Realm - If it is set in /radius menu, it is included in every RADIUS request as Mikrotik-Realm attribute. If it is not set, the same value is sent as in MS-CHAP-Domain attribute (if MS-CHAP-Domain is missing, Realm is not included neither) 

- WISPr-Location-ID - text string specified in radius-location-id property of the HotSpot server WISPr-Location-Name - text string specified in radius-location-name property of the HotSpot server WISPr-Logoff-URL - full link to the login page (for example, http://10.48.0.1/lv/logout) 

Depending on authentication methods (NOTE: HotSpot uses CHAP by default and may use also PAP if unencrypted passwords are enabled, it can not use MSCHAP). 

User-Password - encrypted password (used with PAP authentication) 

- CHAP-Password , CHAP-Challenge - encrypted password and challenge (used with CHAP authentication) 

- MS-CHAP-Response , MS-CHAP-Challenge - encrypted password and challenge (used with MS-CHAPv1 authentication) MS-CHAP2-Response , MS-CHAP-Challenge - encrypted password and challenge (used with MS-CHAPv2 authentication)
