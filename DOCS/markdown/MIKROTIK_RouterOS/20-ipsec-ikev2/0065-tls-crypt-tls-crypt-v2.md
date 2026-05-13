## Tls-crypt, tls-crypt v2 

To improve TLS auth, Tls-crypt is added in version 7.17rc3. 

Tls-crypt, tls-crypt v2 is suppoorted only for ovpn client with following settings: 

“auth SHA256” and no key-direction in server configuration, 

1245 

“auth SHA256” and “key-direction 1” in client configuration is needed for authentication to work. 

Example configuration files: 

client-1.ovpn server-1.conf
