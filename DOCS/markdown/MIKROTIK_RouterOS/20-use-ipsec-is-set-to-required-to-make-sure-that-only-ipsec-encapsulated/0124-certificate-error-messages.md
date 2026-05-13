## Certificate Error Messages 

When SSL handshake fails, you will see one of the following certificate errors: 

certificate is not yet valid - notBefore certificate date is after the current time; certificate has expired - certificate expiry date is before the current time; 

cinvalid certificate purpose - the supplied certificate cannot be used for the specified purpose; 

- cself signed certificate in a chain - the certificate chain could be built up using the untrusted certificates but the root could not be found locally; cunable to get issuer certificate locally - CA certificate is not imported locally; 

- cserver's IP address does not match certificate - server address verification is enabled, but the address provided in certificate does not match the server's address;
