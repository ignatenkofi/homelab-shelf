## Limitations 

ROS has its own ovpn implementation , not all ovpn features are supported and not all unsupported are listed. Currently, noteable unsupported OpenVPN features: 

LZO compression. **DEPRECATED** Compression is generally not recommended. VPN tunnels which use compression are susceptible to the VORALCE attack vector. 

NCP autonegotiation, cipher has to been specified in .ovpn file when connecting to an ROS ovpn server. 

OpenVPN username is limited to 27 characters and the password to 233 characters. Password cap increased in 7.18_ab253 to 1000 characters.
