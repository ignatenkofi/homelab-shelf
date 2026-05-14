## Understanding Map ranges 

In order to avoid defining all possible PCP and DSCP mappings, RouterOS allows setting multiple values and ranges for PCP and DSCP values for QoS Profile mapping. 

In the following example, PCP values 0 and 2 use the default QoS profile, 1, 3-4 - streaming, 5 - voip, and 6-7 - control. 

```
/interface ethernet switch qos map vlan
add pcp=1,3-4 profile=streaming
add pcp=5 profile=voip
add pcp=6-7 profile=control
```
