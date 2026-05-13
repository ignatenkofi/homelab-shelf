## CAP Configuration 

When an AP is configured to be controlled by CAPsMAN, configuration of the managed wireless interfaces on the AP is ignored (exceptions: antenna-gain, antenna-mode). Instead, AP accepts configuration for the managed interfaces from CAPsMAN. 

**==> picture [13 x 13] intentionally omitted <==**

The CAP wireless interfaces that are managed by CAPsMAN and whose traffic is being forwarded to CAPsMAN (ie. they are not in local forwarding mode), are shown as disabled, with the note Managed by CAPsMAN . Those interfaces that are in local forwarding mode (traffic is locally managed by CAP, and only management is done by CAPsMAN) are not shown disabled, but the note Managed by CAPsMAN is shown 

CAP behavior of AP is configured in /interface wireless cap menu. From there you can: 

Disable or enable CAP feature on the device 

Set list of wireless interfaces to be controlled by Manager 

- Set list of interfaces over which CAP should attempt to discover Manager Set list of Manager IP addresses that CAP will attempt to contact during discovery Set list of Manager names that CAP will attempt to connect 

Set list of Manager certificate CommonNames that CAP will connect to Set bridge to which interfaces should be added when local forwarding mode is used 

Each wireless interface on a CAP that is under CAPsMAN control appears as a virtual interface on the CAPsMAN. This provides maximum flexibility in data forwarding control using regular RouterOS features, such as routing, bridging, firewall, etc.CAPsMAN Configuration Concepts 

1478 

Many wireless interface settings are able to be grouped together into named groups ('profiles') that simplifies the reuse of configuration - for example, common configuration settings can be configured in a 'configuration profile' and multiple interfaces can then refer to that profile. At the same time any profile setting can be overridden directly in an interface configuration for maximum flexibility. 

Currently there are the following setting groups: 

channel - channel related settings, such as frequency and width 

- datapath - data forwarding related settings, such as bridge to which particular interface should be automatically added as port security - security related settings, such as allowed authentication types or passphrase 

- configuration - main wireless settings group, includes settings such as SSID, and additionally binds together other setting groups - that is, configuration profile can refer to channel, security, etc. named setting groups. Additionally any setting can be overridden directly in configuration profile. 

Interface settings bind together all setting groups, but additionally any setting can be overridden directly in interface settings. 

By means of setting groups, configuration is organized in hierarchical structure with interface (actual user of configuration) as the root. In order to figure out the effective value of some setting this structure is consulted in a fashion where a higher level setting value overrides a lower level value. 

For example, when WPA2 passphrase to be used by a particular interface needs to be found, the following places are consulted and the first place with WPA2 passphrase configured specifies effective passphrase. "->" denotes referring to setting profile (if configured): 

- interface passphrase interface->security passphrase interface->configuration passphrase interface->configuration->security passphrase 

There are 2 types of interfaces on CAPsMAN - "master" and "slave". The master interface holds the configuration for an actual wireless interface (radio), while a slave interface links to the master interface and is intended to hold the configuration for a Virtual-AP (multiple SSID support). There are settings that are meaningful only for master interface, i.e. mainly hardware setup related settings such as radio channel settings. Note that in order for a radio to accept clients, it's master interface needs to be enabled. Slave interfaces will become operational only if enabled and the master interface is enabled. 

Interfaces on CAPsMAN can be static or dynamic. Static interfaces are stored in RouterOS configuration and will persist across reboots. Dynamic interfaces exist only while a particular CAP is connected to CAPsMAN.
