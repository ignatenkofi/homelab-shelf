## Priority from DSCP 

Another way of setting VLAN or WMM priority is by using the DSCP field in the IP header, this can only be done by the IP firewall mangle rule with `newpriority=from-dscp` or `new-priority=from-dscp-high-3-bits` settings and `set-priority` action property. Note that DSCP in the IP header can have values 0-63, but priority only 0-7. When using the `new-priority=from-dscp` setting, the priority will be 3 low bits of the DSCP value, but when using `new-priority=from-dscp-high-3-bits` the priority will be 3 high bits of DSCP value. 

Remember that DSCP can only be accessed on IP packets and the DSCP value in the IP header should be set somewhere (either by client devices or IP mangle rules). 

It is best to set the DSCP value in the IP header of packets on some border router (e.g. main router used for connection to the Internet), based on traffic type e.g. set DSCP value for packets coming from the Internet belonging to SIP connections to 7, and 0 for the rest. This way packets must be marked only in one place. Then all APs on the network can set packet priority from the DSCP value with just one rule.
