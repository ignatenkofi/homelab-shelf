## Properties 

**==> picture [516 x 242] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP/IPv6  If the remote peer's address matches this prefix, then the peer configuration is used in authentication and establishment of  Phase<br>Prefix; Default:  0.0.0 1 . If several peer's addresses match several configuration entries, the most specific one (i.e. the one with the largest netmask)<br>.0/0 ) will be used.<br>comment  (string;  Short description of the peer.<br>Default: )<br>disabled  (yes | no;  Whether peer is used to matching remote peer's prefix.<br>Default:  no )<br>exchange-mode  (ag Different ISAKMP phase 1 exchange modes according to RFC 2408. the  main  mode relaxes rfc2409 section 5.4, to allow pre-<br>gressive | base |  shared-key authentication in the main mode. ike2 mode enables Ikev2 RFC 7296. Parameters that are ignored by IKEv2<br>main | ike2; Default:  proposal-check, compatibility-options, lifebytes, dpd-maximum-failures, nat-traversal.<br>main )<br>local-address  (IP Routers local address on which Phase 1 should be bounded to.<br>/IPv6 Address;<br>Default: )<br>name  (string;<br>Default: )<br>**----- End of picture text -----**<br>


1197 

**==> picture [516 x 226] intentionally omitted <==**

**----- Start of picture text -----**<br>
passive  (yes | no;  When a passive mode is enabled will wait for a remote peer to initiate an IKE connection. The enabled passive mode also<br>Default:  no ) indicates that the peer is xauth responder, and disabled passive mode - xauth initiator. When a passive mode is a disabled peer<br>will try to establish not only phase1 but also phase2 automatically, if policies are configured or created during the phase1.<br>port  (integer:0.. Communication port used (when a router is an initiator) to connect to remote peer in cases if remote peer uses the non-default<br>65535; Default:  500 ) port.<br>profile  (string;  Name of the profile template that will be used during IKE negotiation.<br>Default:  default )<br>send-initial-contact  ( Specifies whether to send "initial contact" IKE packet or wait for remote side, this packet should trigger the removal of old peer<br>yes | no; Default:  yes SAs for current source address. Usually, in road warrior setups clients are initiators and this parameter should be set to no. Initial<br>) contact is not sent if modecfg or xauth is enabled for ikev1.<br>Read-only properties<br>Property Description<br>dynamic  (yes | no) Whether this is a dynamically added entry by a different service (e.g L2TP).<br>responder  (yes | no) Whether this peer will act as a responder only (listen to incoming requests) and not initiate a connection.<br>**----- End of picture text -----**<br>
