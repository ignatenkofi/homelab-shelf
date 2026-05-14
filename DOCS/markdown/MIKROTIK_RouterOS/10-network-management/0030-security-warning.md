## Security warning 

The URL is randomly generated, so while it is available to anyone who knows the link, if you keep it safe, only people with the link will be able to use it. 

File share uses HTTPS (TCP port 443), but if you have manually configured WebFig to also use HTTPS, File Share will then automatically work only though our cloud relay service, since there can not be two things using the same port in one device. By default www-ssl is not enabled, so File Share works directly by default, without using the relay for downloads. Enabling file share will not in any way affect your WebFig confguration and will not open it to the world. 

In the case of the File Share feature, when a user wants to share a file with somebody, this is the order of operation, if your router is directly accessible from the internet (checked by the Relay server): 

Router locally generates private key and certificate 

- Signing of certificate is performed on router using standard ACME protocol (using DNS-01 challenge with LetsEncrypt backend) DNS-01 challenge is sent to MikroTik cloud DNS server, by temporarily adding a DNS TXT record (standard procedure) DNS name resolves to router 

Secure 443 port is opened with private certificate
