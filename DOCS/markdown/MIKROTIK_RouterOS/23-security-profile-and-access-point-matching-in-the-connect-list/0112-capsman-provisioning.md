## CAPsMAN provisioning 

CAPsMAN distinguishes between CAPs based on a common-name identifier. The identifier is generated based on the following rules: 

if CAP provided a certificate, the identifier is set to the Common Name field in the certificate otherwise, an identifier is based on Base-MAC provided by CAP in the form: '[XX:XX:XX:XX:XX:XX]'. 

When the DTLS connection with CAP is successfully established (which means that CAP identifier is known and valid), CAPsMAN makes sure there is no stale connection with CAP using the same identifier. Currently connected CAPs are listed in /caps-man remote-cap menu: 

```
[admin@CM] /caps-man> remote-cap print
```

```
# ADDRESS IDENT STATE RADIOS 0 00:0C:42:00:C0:32/27044 MT-000C4200C032 Run 1
```

CAPsMAN distinguishes between actual wireless interfaces (radios) based on their built-in MAC address (radio-mac). This implies that it is impossible to manage two radios with the same MAC address on one CAPsMAN. Radios currently managed by CAPsMAN (provided by connected CAPs) are listed in /c aps-man radio menu: 

```
[admin@CM] /caps-man> radio print
Flags: L - local, P - provisioned
# RADIO-MAC INTERFACE REMOTE-AP-IDENT
0 P 00:03:7F:48:CC:07 cap1 MT-000C4200C032
```

When CAP connects, CAPsMAN at first tries to bind each CAP radio to CAPsMAN master interface based on radio-mac. If an appropriate interface is found, radio gets set up using master interface configuration and configuration of slave interfaces that refer to a particular master interface. At this moment interfaces (both master and slaves) are considered bound to radio and radio is considered provisioned. 

If no matching master interface for radio is found, CAPsMAN executes 'provisioning rules'. Provisioning rules is an ordered list of rules that contain settings that specify which radio to match and settings that specify what action to take if a radio matches. 

Provisioning rules for matching radios are configured in /caps-man provisioning menu: 

**==> picture [506 x 302] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (create-disabled | create-enabled |  Action to take if rule matches are specified by the following settings:<br>create-dynamic-enabled | none; Default: none )<br>create-disabled  - create disabled static interfaces for radio. I.e., the interfaces will be bound to<br>the radio, but the radio will not be operational until the interface is manually enabled;<br>create-enabled  - create enabled static interfaces. I.e., the interfaces will be bound to the radio<br>and the radio will be operational;<br>create-dynamic-enabled  - create enabled dynamic interfaces. I.e., the interfaces will be bound<br>to the radio, and the radio will be operational;<br>none  - do nothing, leaves radio in the non-provisioned state;<br>comment  (string; Default: ) Short description of the Provisioning rule<br>common-name-regexp  (string; Default: ) Regular expression to match radios by common name. Each CAP's common name identifier can<br>be found under "/caps-man radio" as value "REMOTE-CAP-NAME"<br>hw-supported-modes  (a|a-turbo|ac|an|b|g|g- Match radios by supported wireless modes<br>turbo|gn; Default: )<br>identity-regexp  (string; Default: ) Regular expression to match radios by router identity<br>ip-address-ranges  (IpAddressRange[, Match CAPs with IPs within configured address range.<br>IpAddressRanges] max 100x; Default: "" )<br>master-configuration  (string; Default: ) If action specifies to create interfaces, then a new master interface with its configuration set to this<br>configuration profile will be created<br>**----- End of picture text -----**<br>


1469 

name-format (cap | identity | prefix | prefixspecify the syntax of the CAP interface name creation identity; Default: cap ) cap - default name identity - CAP boards system identity name prefix - name from the name-prefix value prefix-identity - name from the name-prefix value and the CAP boards system identity name name-prefix (string; Default: ) name prefix which can be used in the name-format for creating the CAP interface names radio-mac (MAC address; Default: 00:00:00:00: MAC address of radio to be matched, empty MAC (00:00:00:00:00:00) means match all MAC 00:00 ) addresses slave-configurations (string; Default: ) If action specifies to create interfaces, then a new slave interface for each configuration profile in this list is created. 

**==> picture [13 x 13] intentionally omitted <==**

If no rule matches radio, then implicit default rule with action create-enabled and no configurations set is executed. 

To get the active provisioning matchers: 

```
[admin@CM] /caps-man provisioning> print
Flags: X - disabled
0 radio-mac=00:00:00:00:00:00 action=create-enabled master-configuration=main-cfg
slave-configurations=virtual-ap-cfg name-prefix=""
```

For the user's convenience there are commands that allow the re-execution of the provisioning process for some radio or all radios provided by some AP: 

```
[admin@CM] > caps-man radio provision 0
```
