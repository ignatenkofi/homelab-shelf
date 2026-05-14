## CAP to CAPsMAN Connection 

For the CAPsMAN system to function and provide wireless connectivity, a CAP must establish management connection with CAPsMAN. A management connection can be established using MAC or IP layer protocols and is secured using 'DTLS'. 

A CAP can also pass the client data connection to the Manager, but the data connection is not secured. If this is deemed necessary, then other means of data security needs to be used, e.g. IPSec or encrypted tunnels. 

CAP to CAPsMAN connection can be established using 2 transport protocols (via Layer 2 and Layer3). 

MAC layer connection features: 

no IP configuration necessary on CAP 

CAP and CAPsMAN must be on the same Layer 2 segment - either physical or virtual (by means of L2 tunnels) 

- IP layer (UDP) connection features: 

can traverse NAT if necessary 

CAP must be able to reach CAPsMAN using IP protocol 

if the CAP is not on the same L2 segment as CAPsMAN, it must be provisioned with the CAPsMAN IP address, because IP multicast based discovery does not work over Layer3 

In order to establish connection with CAPsMAN, CAP executes a discovery process. During discovery, CAP attempts to contact CAPsMAN and builds an available CAPsMANs list. CAP attempts to contact to an available CAPsMAN using: 

configured list of Manager IP addresses 

list of CAPsMAN IP addresses obtained from DHCP server 

broadcasting on configured interfaces using both - IP and MAC layer protocols. 

When the list of available CAPsMANs is built, CAP selects a CAPsMAN based on the following rules: 

- if caps-man-names parameter specifies allowed manager names ( /system identity of CAPsMAN), CAP will prefer the CAPsMAN that is earlier in the list, if list is empty it will connect to any available Manager suitable Manager with MAC layer connectivity is preferred to Manager with IP connectivity 

After Manager is selected, CAP attempts to establish DTLS connection. There are the following authentication modes possible: 

no certificates on CAP and CAPsMAN - no authentication 

1476 

only Manager is configured with certificate - CAP checks CAPsMAN certificate, but does not fail if it does not have appropriate trusted CA certificate, CAPsMAN must be configured with require-peer-certificate=no in order to establish connection with CAP that does not possess certificate 

CAP and CAPsMAN are configured with certificates - mutual authentication 

After DTLS connection is established, CAP can optionally check CommonName field of certificate provided by CAPsMAN. caps-man-certificate-commonnames parameter contains list of allowed CommonName values. If this list is not empty, CAPsMAN must be configured with certificate. If this list is empty, CAP does not check CommonName field. 

If the CAPsMAN or CAP gets disconnected from the network, the loss of connection between CAP and CAPsMAN will be detected in approximately 10-20 seconds.
