## ANQP elements 

Access network query protocol (ANQP). Not all necessary information is included in probe response and beacon frames. For client device to get more information before choosing access point to associate with ANQP is used. The Access Point can have stored information in multiple ANQP elements. Client device will use ANQP to query only for the information it is interested in. This reduces the time needed before association. 

**==> picture [504 x 177] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>3gpp-raw  (octet string in hex; Default: ) Cellular network advertisement information - country and network codes. This helps<br>Hotspot 2.0 clients in the selection of an Access Point to access 3GPP network. Please<br>see 3GPP TS 24.302. (Annex H) for a format of this field. This value is sent ANQP<br>response if queried.<br>3gpp-info  (number/number; Default: ) Cellular network advertisement information - country and network codes. This helps<br>Hotspot 2.0 clients in the selection of an Access Point to access 3GPP network.  Written<br>as "mcc/mnc". Multiple mcc/mnc pairs can be defined, by separating them with a comma.<br>authentication-types  (dns-redirection: url | https- This property is only effective when asra is set to yes . Value of url is optional and not<br>redirection: url | online-enrollment: url | terms-and- needed if dns-redirection or online-enrollment is selected. To set the value of u<br>conditions: url ; Default: ) rl to empty string use double quotes. For example:<br>authentication-types=online-enrollment:""<br>**----- End of picture text -----**<br>


1382 

**==> picture [504 x 669] intentionally omitted <==**

**----- Start of picture text -----**<br>
connection-capabilities  (number:number: This option allows to provide information about the allowed IP protocols and ports. This<br>closed|open|unknown; Default: ) information can be provided in ANQP response. The first number represents the IP<br>protocol number, the second number represents a port number.<br>closed  - set if protocol and port combination is not allowed;<br>open  - set if protocol and port combination is allowed;<br>unknown  - set if protocol and port combination is either open or closed.<br>Example:<br>connection-capabilities=6:80:open,17:5060:closed<br>Setting such a value on an Access Point informs the Wireless client, which is connecting<br>to the Access Point, that HTTP (6 - TCP, 80 - HTTP) is allowed and VoIP (17 - UDP;<br>5060 - VoIP) is not allowed.<br>This property does not restrict or allow usage of these protocols and ports, it only gives<br>information to station device which is connecting to Access Point.<br>domain-names  (list of strings; Default: ) None or more fully qualified domain names (FQDN) that indicate the entity operating the<br>Hotspot. A station that is connecting to the Access Point can request this AQNP property<br>and check if there is a suffix match with any of the domain names it has credentials to.<br>ipv4-availability  (double-nated | not-available | port- Information about what IPv4 address and access are available.<br>restricted | port-restricted-double-nated | port-restricted-<br>single-nated | public | single-nated | unknown; Default: n not-available  - Address type not available;<br>ot-available ) public  - public IPv4 address available;<br>port-restricted  - port-restricted IPv4 address available;<br>single-nated  - single NATed private IPv4 address available;<br>double-nated  - double NATed private IPv4 address available;<br>port-restricted-single-nated  -port-restricted IPv4 address and single<br>NATed IPv4 address available;<br>port-restricted-double-nated  - port-restricted IPv4 address and double<br>NATed IPv4 address available;<br>unknown  - availability of the address type is not known.<br>ipv6-availability  (available | not-available | unknown;  Information about what IPv6 address and access are available.<br>Default: not-available )<br>not-available  - Address type not available;<br>available  - address type available;<br>unknown  - availability of the address type is not known.<br>realms  (string:eap-sim|eap-aka|eap-tls|not-specified;  Information about supported realms and the corresponding EAP method.<br>Default: ) realms=example.com:eap-tls,foo.ba:not-specified<br>realms-raw  (octet string in hex; Default: ) Set NAI Realm ANQP-element manually.<br>roaming-ois  (octet string in hex; Default: ) Organization identifier (OI) usually are 24-bit is unique identifiers like organizationally<br>unique identifier (OUI) or company identifier (CID). In some cases, OI is longer for<br>example OUI-36.<br>A subscription service provider (SSP) can be specified by its OI. roaming-ois property<br>can contain zero or more SSPs OIs whose networks are accessible via this AP. Length of<br>OI should be specified before OI itself. For example, to set E4-8D-8C and 6C-3B-6B:<br>roaming-ois=03E48D8C036C3B6B<br>venue-names  (string:lang; Default: ) Venue name can be used to provide additional info on the venue. It can help the client to<br>choose a proper Access Point.<br>Venue-names parameter consists of zero or more duple that contain Venue Name and<br>Language Code:<br>venue-names=CoffeeShop:eng,TiendaDeCafe:es<br>The Language Code field value is a two or three-character 8 language code selected<br>from ISO-639.<br>**----- End of picture text -----**<br>


Realms raw 

1383 

realms-raw - list of strings with hex values. Each string specifies contents of "NAI Realm Tuple", excluding "NAI Realm Data Field Length" field. 

Each hex encoded string must consist of the following fields: 

```
- NAI Realm Encoding (1 byte)
- NAI Realm Length (1 byte)
- NAI Realm (variable)
- EAP Method Count (1 byte)
- EAP Method Tuples (variable)
```

For example, value "00045465737401020d00" decodes as: 

```
- NAI Realm Encoding: 0 (rfc4282)
- NAI Realm Length: 4
- NAI Realm: Test
- EAP Method Count: 1
- EAP Method Length: 2
- EAP Method Tuple: TLS, no EAP method parameters
```

Note, that setting "realms-raw=00045465737401020d00" produces the same advertisement contents as setting "realms=Test:eap-tls". 

Refer to 802.11-2016, section 9.4.5.10 for full NAI Realm encoding.
