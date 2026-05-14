## Connection Terminating from RADIUS 

Sub-menu: **`/radius incoming`** 

This facility supports unsolicited messages sent from the RADIUS server. Unsolicited messages extend RADIUS protocol commands, that allow terminating a session that has already been connected from the RADIUS server. For this purpose, DM (Disconnect-Messages) is used. Disconnect messages cause a user session to be terminated immediately. 

**==> picture [13 x 13] intentionally omitted <==**

RouterOS doesn't support POD (Packet of Disconnect) the other RADIUS access request packet that performs a similar function as Disconnect Messages
