## Security profile and access point matching in the connect list 

Client uses value of connect-list security-profile property to match only those access points that support necessary security. 

mode =static-keys-required and mode =static-keys-optional matches only access points with the same mode in interface security-profile . If mode =dynamic-keys, then connect list entry matches if all of the authentication-types , unicast-ciphers and group-ciphers contain at least one value that is advertised by access point.
