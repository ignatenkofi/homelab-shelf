## CAP configuration 

Menu: /interface/wifi/cap 

**==> picture [516 x 284] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>caps-man-addresses  list of IP ( List of Manager IP addresses that CAP will attempt to contact during discovery<br>addresses; Default:  empty )<br>caps-man-names () An ordered list of CAPs Manager names that the CAP will connect to, if empty - CAP does not check Manager name<br>discovery-interfaces (list of  List of interfaces over which CAP should attempt to discover Manager<br>interfaces;)<br>lock-to-caps-man (no | yes;  Sets, if CAP should lock to the first CAPsMAN it connects to<br>Default:  no )<br>slaves-static () Creates Static Virtual Interfaces, allows the possibility to assign IP configuration to those interfaces. MAC address is<br>used to remember each static-interface when applying the configuration from the CAPsMAN.<br>caps-man-certificate-common- List of Manager certificate CommonNames that CAP will connect to, if empty - CAP does not check Manager<br>names  () certificate CommonName<br>certificate  () Certificate to use for authenticating<br>enabled  (yes | no; Default:  no ) Disable or enable the CAP feature<br>current-caps-man-address () Shows currently used CAPsMAN address (available since 7.15)<br>current-caps-man-identity () Shows currently used CAPsMAN identity (available since 7.15)<br>slaves-datapath  ()<br>**----- End of picture text -----**<br>


1366
