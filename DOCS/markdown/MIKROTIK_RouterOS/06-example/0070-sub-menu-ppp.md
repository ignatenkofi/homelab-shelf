## Sub-menu: `/ppp` 

The MikroTik RouterOS provides scalable Authentication, Authorization, and Accounting (AAA) functionality. 

Local authentication is performed using the User Database and the Profile Database. The actual configuration for the given user is composed using the respective user record from the User Database, the associated item from the Profile Database, and the item in the Profile database which is set as default for a given service the user is authenticating to. Default profile settings from the Profile database have the lowest priority while the user access record settings from the User Database have the highest priority with the only exception being particular IP addresses take precedence over IP pools in the localaddress and remote-address settings, which are described later on. 

Support for RADIUS authentication gives the ISP or network administrator the ability to manage PPP user access and accounting from one server throughout a large network. The MikroTik RouterOS has a RADIUS client that can authenticate for PPP, PPPoE, PPTP, L2TP, OPVN, and ISDN connections. The attributes received from the RADIUS server override the ones set in the default profile, but if some parameters are not received they are taken from the respective default profile.
