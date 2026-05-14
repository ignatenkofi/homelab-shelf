## DSCP from Priority 

Similarly, the DSCP value can be set if the received packet contains VLAN or WMM priority. This can be achieved with IP mangle rules with `newdscp=from-priority` or `new-dscp=from-priority-to-high-3-bits` settings and `change-dscp` action property. Note that priority in VLAN or WMM packets can have values 0-7, but DSCP in IP headers are 0-63. When using the `new-dscp=from-priority` setting, the value of priority will set the 3 low bits of the DSCP, but when using `new-dscp=from-priority-to-high-3-bits` the value of priority will set the 3 high bits of the DSCP. 

However, this setting cannot directly use ingress priority from received VLAN or WMM packets. You first need to set priority using IP mangle or bridge filter /nat rules (ingress priority can be used in this case), and only then apply the DSCP rule. 

627
