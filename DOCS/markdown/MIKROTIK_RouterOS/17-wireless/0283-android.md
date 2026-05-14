## Android 

When connecting to a network with EAP authentication, Android devices ask the user to specify a 'domain'. This refers to the expected domain of the host name included in the RADIUS server's TLS certificate ( 'mikrotik.test' in our example). 

By default, Android devices use the device's built-in root CA list for validating the RADIUS server's certificate. When using your own CA, it needs to be selected in the appropriate dropdown menu.
