## Set DSCP from VLAN or WMM priority 

In this example, the AP device needs to set DSCP from WMM priority when packets are routed. First, add a rule to set priority, it will be needed for the DSCP rule to correctly change the DSCP value. This rule can take priority from ingress. Then add the DSCP rule to change its value.
