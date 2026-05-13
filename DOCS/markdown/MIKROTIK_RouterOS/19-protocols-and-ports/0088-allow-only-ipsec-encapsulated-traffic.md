## Allow only IPsec encapsulated traffic 

There are some scenarios where for security reasons you would like to drop access from/to specific networks if incoming/outgoing packets are not encrypted. For example, if we have L2TP/IPsec setup we would want to drop nonencrypted L2TP connection attempts. 

There are several ways how to achieve this: 

Using IPsec policy matcher in firewall; 

Using generic IPsec policy with action set to drop and lower priority (can be used in Road Warrior setups where dynamic policies are generated); By setting DSCP or priority in mangle and matching the same values in firewall after decapsulation.
