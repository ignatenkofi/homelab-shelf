## RADIUS MAC authentication 

Note: RAIDUS MAC authentication is used by access point for clients that are not found in the access-list, similarly to the default-authentication property of the wireless interface. It controls whether client is allowed to proceed with authentication, or is rejected immediately. 

- When radius-mac-authentication =yes, access point queries RADIUS server by sending Access-Request with the following attributes: User-Name - Client MAC address. This is encoded as specified by the radius-mac-format setting. Default encoding is "XX:XX:XX:XX:XX:XX". Nas-Port-Id - name of wireless interface. User-Password - When radius-mac-mode =as-username-and-password this is set to the same value as User-Name. Otherwise this attribute is empty. 

   - Calling-Station-Id - Client MAC address, encoded as "XX-XX-XX-XX-XX-XX". 

   - Called-Station-Id - MAC address and SSID of the access point, encoded as "XX-XX-XX-XX-XX-XX:SSID" (minus separated pairs of MAC address digits, followed by colon, followed by SSID value). 

   - Acct-Session-Id - Added when radius-mac-accounting =yes. 

1418 

When access point receives Access-Accept or Access-Reject response from the RADIUS server, it stores the response and either allows or rejects client. Access point uses following RADIUS attributes from the Access-Accept response: 

- Ascend-Data-Rate 

- Ascend-Xmit-Rate Mikrotik-Wireless-Forward - Same as access-list forwarding . Mikrotik-Wireless-Enc-Algo - Same as access-list private-algo . Mikrotik-Wireless-Enc-Key - Same as access-list private-key . Mikrotik-Wireless-Psk - Same as access-list private-pre-shared-key . Mikrotik-Wireless-Mpkey - Same as Management-protection-key in Access list Session-Timeout - Time, after which client will be disconnected. 

- Acct-Interim-Interval - Overrides value of interim-update . Class - If present, value of this attribute is saved and included in Accounting-Request messages.
