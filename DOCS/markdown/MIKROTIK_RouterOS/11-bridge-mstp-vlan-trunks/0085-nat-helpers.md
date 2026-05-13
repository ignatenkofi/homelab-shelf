## NAT Helpers 

Hosts behind a NAT-enabled router do not have true end-to-end connectivity. Therefore some Internet protocols might not work in scenarios with NAT. To overcome these limitations RouterOS includes a number of NAT helpers, that enable NAT traversal for various protocols. 

Nat helpers can be managed from `/ip firewall service-ports` menu. 

List of available nat helpers: 

**==> picture [479 x 250] intentionally omitted <==**

**----- Start of picture text -----**<br>
Helper Description<br>FTP FTP service helper<br>H323 H323 service helper<br>IRC IRC service helper<br>PPTP PPTP (GRE) tunneling helper<br>UDPLITE UDP-Lite service helper<br>DCCP DCCP service helper<br>SCTP SCTP service helper<br>SIP SIP helper. Additional options:<br>sip-direct-media  allows redirecting the RTP media stream to go directly from the caller to the callee. The default value is yes.<br>sip-timeout  allows adjusting TTL of SIP UDP connections. Default: 1 hour. In some setups, you have to reduce that.<br>TFTP TFTP service helper<br>RSTP RTSP service helper<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

If connection tracking is not enabled then firewall service ports will be shown as inactive 

**==> picture [13 x 13] intentionally omitted <==**

udplite , dccp , and sctp are built-in services of the connection tracking. Since these are not separately loaded modules, they cannot be disabled separately, they got disabled together with the connection tracking.
