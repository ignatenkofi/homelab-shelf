## Certificates 

To set up a secure SSTP tunnel, certificates are required. On the server, authentication is done only by username and password, but on the client - the server is authenticated using a server certificate. It is also used by the client to cryptographically bind SSL and PPP authentication, meaning - the clients send a special value over SSTP connection to the server, this value is derived from the key data that is generated during PPP authentication and server certificate, this allows the server to check if both channels are secure. 

If SSTP clients are on Windows PCs then the only way to set up a secure SSTP tunnel when using a self-signed certificate is by importing the "server" certificate on the SSTP server and on the Windows PC adding a CA certificate in the trusted root. 

1265 

**==> picture [13 x 13] intentionally omitted <==**

If your server certificate is issued by a CA which is already known by Windows, then the Windows client will work without any additional certificate imports to a trusted root. 

**==> picture [13 x 13] intentionally omitted <==**

RSA key length must be at least 472 bits if a certificate is used by SSTP. Shorter keys are considered as security threats. 

A similar configuration on RouterOS client would be to import the CA certificate and enabling the verify-server-certificate option. In this scenario, Man-inthe-Middle attacks are not possible. 

Between two Mikrotik routers, it is also possible to set up an insecure tunnel by not using certificates at all. In this case, data going through the SSTP tunnel is using anonymous DH and Man-in-the-Middle attacks are easily accomplished. This scenario is not compatible with Windows clients. 

It is also possible to make a secure SSTP tunnel by adding additional authorization with a client certificate. Configuration requirements are: 

certificates on both server and client 

verification options enabled on server and client 

This scenario is also not possible with Windows clients, because there is no way to set up a client certificate on Windows.
