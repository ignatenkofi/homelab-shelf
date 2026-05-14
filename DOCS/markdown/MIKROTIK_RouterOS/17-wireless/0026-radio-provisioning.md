## Radio Provisioning 

Once configuration templates have been created, you can select which devices should be provisioned with each of the template. Of course, in simple setups it is enough to have only one provisioning rule, but if you wish to send one configuration to 2.4GHz interfaces and a different one to 5GHz interfaces, you can create two provisioning rules and define, which template is sent where, using `supported-bands` parameter. 

CAPsMAN distinguishes between actual wireless interfaces (radios) based on their built-in MAC address (radio-mac). This implies that it is impossible to manage two radios with the same MAC address on one CAPsMAN. Radios currently managed by CAPsMAN (provided by connected CAPs) are listed in **`/ interface/wifi/radio`** menu, this list will also include the built-in wifi interfaces that are present on CAPsMAN itself if there are any: 

```
[admin@c52i] > interface/wifi/radio/print
Flags: L - LOCAL
Columns: CAP, RADIO-MAC, INTERFACE
#   CAP                  RADIO-MAC          INTERFACE
0 L                      18:FD:74:AF:F4:28  wifi1
1 L                      18:FD:74:AF:F4:29  wifi2
2   hapAX3@192.168.88.30  48:A9:8A:0B:F7:4B  cap1
```

When CAP connects, CAPsMAN at first tries to bind each CAP radio to CAPsMAN master interface based on radio-mac. If an appropriate interface is found, the radio gets set up using master interface configuration and configuration of slave interfaces that refer to a particular master interface. At this moment interfaces (both master and slaves) are considered bound to radio and radio is considered provisioned. This happens only if there were matching static entries already present under `/interface/wifi` , typically if the entry was made previously either manually, or with provisioning rules that contain action "create-enabled" or "create-disabled". 

If no matching master interface for radio is found, CAPsMAN executes 'provisioning rules', which are defined under `/interface/wifi/provisioning/` . Provisioning rules is an ordered list of rules that contain settings that specify which radio to match and settings that determine what action to take if a radio matches. 

When CAP joins CAPsMAN, and there is no matching interface for it present under `/interface/wifi` , provisioning rules will automatically be checked, once a match is found, the CAP's wireless interface will appear under `/interface/wifi` . Such an interface is "provisioned", provisioned in this context means that there is a wifi interface present for the radio, and it has a configuration profile assigned to it. 

There is also an option to manually provision interfaces, which will make CAPsMAN start evaluating provisioning rules against the specific interface, and a new interface will be created upon match. If there was already an entry present for the radio under `/interface/wifi/` , that entry will be deleted and recreated. Manual provisioning re-creates the interface and is generally not needed , since provisioning rules are evaluated automatically, and if you change the configuration profile associated with the provisioning rule, the changes will be applied to all wifi interfaces that use that configuration. If you manually provision interfaces, the interface ID or name can change, resulting in broken references to other objects, for example, bridge ports. 

Manual provision can be done under `/interface/wifi/capsman/remote-cap/provision` to provision all radios associated with specific CAPs, it can also be done under `/interface/wifi/radio/provision` , to provision specific radios. 

1343 

CAPsMAN cannot manage it's own wifi interfaces using `configuration.manager=capsman` , it is enough to just set the same configuration profile on local interfaces manually as you would with provisioning rules, and the end result will be the same as if they were CAPs. That being said, it is also possible to provision local interfaces via `/interface/wifi/radio` menu, it should be noted that to regain control of local interfaces after provisioning, you will need to disable the matching provisioning rules and press "provision" again, which will return local interfaces to an unconfigured state. 

**==> picture [13 x 13] intentionally omitted <==**

Provision must be done only initially, and is done automatically upon CAP joining if there are matching provisioning rules that are enabled. If you adjust any configuration profile that is linked to the provisioned interface, all changes will be "pushed" as soon as you apply changes to the profile, with no need to re-create the already existing interface. 

Provisioning itself is not for sending configuration, it is for essentially creating a new interface. In most cases, there is no reason to perform manual provisioning once you already have CAP interfaces running.
