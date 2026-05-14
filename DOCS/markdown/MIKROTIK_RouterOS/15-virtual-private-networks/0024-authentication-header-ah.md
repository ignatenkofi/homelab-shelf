## Authentication Header (AH) 

1191 

AH is a protocol that provides authentication of either all or part of the contents of a datagram through the addition of a header that is calculated based on the values in the datagram. What parts of the datagram are used for the calculation, and the placement of the header depends on whether tunnel or transport mode is used. 

The presence of the AH header allows to verify the integrity of the message but doesn't encrypt it. Thus, AH provides authentication but not privacy. Another protocol (ESP) is considered superior, it provides data privacy and also its own authentication method. 

RouterOS supports the following authentication algorithms for AH: 

SHA2 (256, 512) SHA1 MD5
