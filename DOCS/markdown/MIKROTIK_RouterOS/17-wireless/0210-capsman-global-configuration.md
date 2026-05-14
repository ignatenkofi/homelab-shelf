## CAPsMAN Global Configuration 

Settings to enable CAPsMAN functionality are found in /caps-man manager menu: 

**==> picture [516 x 260] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled  (yes | no; Default:  no ) Disable or enable CAPsMAN functionality<br>certificate  (auto | certificate  Device certificate<br>name | none; Default:  none )<br>ca-certificate  (auto | certificate  Device CA certificate<br>name | none; Default:  none )<br>require-peer-certificate  (yes | no;  Require all connecting CAPs to have a valid certificate<br>Default:  no )<br>package-path  (string |; Default: ) Folder location for the RouterOS packages. For example, use "/upgrade" to specify the upgrade folder from the files<br>section. If empty string is set, CAPsMAN can use built-in RouterOS packages, note that in this case only CAPs with<br>the same architecture as CAPsMAN will be upgraded.<br>upgrade-policy  (none | require- Upgrade policy options<br>same-version | suggest-same-<br>upgrade; Default:  none ) none - do not perform upgrade<br>require-same-version - CAPsMAN suggest to upgrade the CAP RouterOS version and if it fails it will not<br>provision the CAP. (Manual provision is still possible)<br>suggest-same-version - CAPsMAN suggests to upgrade the CAP RouterOS version and if it fails it will still be<br>provisioned<br>**----- End of picture text -----**<br>

Radio Provisioning 

1479 

CAPsMAN distinguishes between CAPs based on an identifier. The identifier is generated based on the following rules: 

if CAP provided a certificate, identifier is set to the Common Name field in the certificate 

otherwise identifier is based on Base-MAC provided by CAP in the form: '[XX:XX:XX:XX:XX:XX]'. 

When the DTLS connection with CAP is successfully established (which means that CAP identifier is known and valid), CAPsMAN makes sure there is no stale connection with CAP using the same identifier. Currently connected CAPs are listed in /caps-man remote-cap menu: 

```
[admin@CM] /caps-man> remote-cap print
# ADDRESS                                    IDENT           STATE               RADIOS
0 00:0C:42:00:C0:32/27044                    MT-000C4200C032 Run                      1
```

CAPsMAN distinguishes between actual wireless interfaces (radios) based on their builtin MAC address (radio-mac). This implies that it is impossible to manage two radios with the same MAC address on one CAPsMAN. Radios currently managed by CAPsMAN (provided by connected CAPs) are listed in /c aps-man radio menu: 

```
[admin@CM] /caps-man> radio print
Flags: L - local, P - provisioned
#    RADIO-MAC         INTERFACE                               REMOTE-AP-IDENT
0  P 00:03:7F:48:CC:07 cap1                                    MT-000C4200C032
```

When CAP connects, CAPsMAN at first tries to bind each CAP radio to CAPsMAN master interface based on radio-mac. If an appropriate interface is found, radio gets set up using master interface configuration and configuration of slave interfaces that refer to particular master interface. At this moment interfaces (both master and slaves) are considered bound to radio and radio is considered provisioned. 

If no matching master interface for radio is found, CAPsMAN executes 'provisioning rules'. Provisioning rules is an ordered list of rules that contain settings that specify which radio to match and settings that specify what action to take if a radio matches. 

Provisioning rules for matching radios are configured in /caps-man provisioning menu: 

**==> picture [516 x 374] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (create-disabled | create-enabled |  Action to take if rule matches are specified by the following settings:<br>create-dynamic-enabled | none; Default:  none )<br>create-disabled  - create disabled static interfaces for radio. I.e., the interfaces will be bound to<br>the radio, but the radio will not be operational until the interface is manually enabled;<br>create-enabled  - create enabled static interfaces. I.e., the interfaces will be bound to the radio<br>and the radio will be operational;<br>create-dynamic-enabled  - create enabled dynamic interfaces. I.e., the interfaces will be bound to<br>the radio, and the radio will be operational;<br>none  - do nothing, leaves radio in non-provisioned state;<br>comment  (string; Default: ) Short description of the Provisioning rule<br>common-name-regexp  (string; Default: ) Regular expression to match radios by common name<br>hw-supported-modes  (a|a-turbo|ac|an|b|g|g- Match radios by supported wireless modes<br>turbo|gn; Default: )<br>identity-regexp  (string; Default: ) Regular expression to match radios by router identity<br>ip-address-ranges  (IpAddressRange[, Match CAPs with IPs within configured address range.<br>IpAddressRanges] max 100x; Default: ) ""<br>master-configuration  (string; Default: ) If  action  specifies to create interfaces, then a new master interface with its configuration set to this<br>configuration profile will be created<br>name-format  (cap | identity | prefix | prefix- specify the syntax of the CAP interface name creation<br>identity; Default:  cap )<br>cap - default name<br>identity - CAP boards system identity name<br>prefix - name from the name-prefix value<br>prefix-identity - name from the name-prefix value and the CAP boards system identity name<br>name-prefix  (string; Default: ) name prefix which can be used in the name-format for creating the CAP interface names<br>**----- End of picture text -----**<br>

1480 

radio-mac (MAC address; Default: 00:00:00:00: MAC address of radio to be matched, empty MAC (00:00:00:00:00:00) means match all MAC 00:00 ) addresses slave-configurations (string; Default: ) If action specifies to create interfaces, then a new slave interface for each configuration profile in this list is created. 

**==> picture [13 x 13] intentionally omitted <==**

If no rule matches radio, then implicit default rule with action create-enabled and no configurations set is executed. 

To get the active provisioning matchers: 

```
[admin@CM] /caps-man provisioning> print
Flags: X - disabled
```

```
0   radio-mac=00:00:00:00:00:00 action=create-enabled master-configuration=main-cfg
    slave-configurations=virtual-ap-cfg name-prefix=""
```

For user's convenience there are commands that allow the re-execution of the provisioning process for some radio or all radios provided by some AP: 

```
[admin@CM] > caps-man radio provision 0
```
