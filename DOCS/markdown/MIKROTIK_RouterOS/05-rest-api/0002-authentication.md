## Authentication 

Authentication to the REST API is performed via HTTP Basic Auth. Provide your Username and password are the same as for the console user (by default "admin" with no password). 

**==> picture [13 x 13] intentionally omitted <==**

You have to set up certificates to use secure HTTPS, if self-signed certs are used, then CA must be imported to the trusted root. However, for testing purposes, it is possible to connect insecurely (for cUrl use -k flag, for wget use --no-check-certificate).
