## Read-only properties 

**==> picture [412 x 117] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>current-endpoint-address  (IP/IPv6) The most recent source IP address of correctly authenticated packets from the peer.<br>current-endpoint-port  (integer) The most recent source IP port of correctly authenticated packets from the peer.<br>last-handshake  (integer) Time in seconds after the last successful handshake.<br>rx  (integer) The total amount of bytes received from the peer.<br>tx  (integer) The total amount of bytes transmitted to the peer.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

When you encounter issues with reply traffic having the wrong source address, using NAT to translate packet source addresses to your loopback interface is a common workaround. This approach helps ensure that the source address is consistent and correct when packets are routed back through the network.
