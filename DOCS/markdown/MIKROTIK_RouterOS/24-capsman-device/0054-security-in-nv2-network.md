## Security in Nv2 network 

Nv2 security implementation has the following features: 

hardware accelerated data encryption using AES-CCM with 128 bit keys; 

- 4-way handshake for key management (similar to that of 802.11i); 

- preshared key authentication method (similar to that of 802.11i); 

periodically updated group keys (used for broadcast and multicast data). 

Being proprietary protocol Nv2 does not use security mechanisms of 802.11, therefore security configuration is different. Interface using Nv2 protocol ignores security-profile setting. Instead, security is configured by the following interface settings: 

Nv2-security - this setting enables/disables use of security in Nv2 network. Note that when security is enabled on AP, it will not accept clients with disabled security. In the same way clients with enabled security will not connect to unsecure APs. 

1507 

Nv2-preshared-key - preshared key to use for authentication. Data encryption keys are derived from preshared key during 4-way handshake. Preshared key must be the same in order for 2 devices to establish connection. If preshared key will differ, connection will time out because remote party will not be able to correctly interpret key exchange messages. 

1508
