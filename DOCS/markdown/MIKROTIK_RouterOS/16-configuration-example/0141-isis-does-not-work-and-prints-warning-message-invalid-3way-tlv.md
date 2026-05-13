## ISIS does not work and prints warning message "invalid 3way tlv" 

This warning indicates that most likely remote neighbor does not comply  to 3-way handshake for point-to-point networks from RFC 5302. For example, on Cisco you have to enable "isis three-way-handshake ietf" on interface to have 15byte TLV. 

1021
