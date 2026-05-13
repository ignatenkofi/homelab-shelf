## Enabling HTTPS and SSL MQTT 

By default, HTTP and MQTT protocols are used. As mentioned previously in the "Networking" section, working with non-SSL HTTP and non-SSL MQTT is not very safe (unless they are used within heavily protected networks with a well-configured firewall/restricted access) and we advise enabling HTTPS and SSL MQTT . 

Please check ThingsBoard documentation for more information → HTTP over SSL and MQTT over SSL guides. 

First of all, there is no SSL without a certificate and one needs to be made (or purchased). 

In short, this section will demonstrate how to generate self-signed certificates for HTTPS and SSL MQTT. Then, you will need to upload them to the correct folder within the ThingsBoard installation and alter the ThingsBoard configuration file accordingly. 

In our guide, we will use RouterOS to generate both certificates (but you can also use OpenSSL or other tools you want).
