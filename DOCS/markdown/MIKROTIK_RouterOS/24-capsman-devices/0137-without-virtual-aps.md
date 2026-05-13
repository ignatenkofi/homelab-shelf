## Without Virtual APs 

Not everyone wants to create Virtual APs since that does decrease the total throughput. If you want to use multiple devices to create multiple SSIDs, then it is possible to assign a certain configuration on a CAP based on its identity. To achieve this you should use CAPsMAN provisioning rules along with RegEx expressions. In this example we are going to assign the Config_WORK configuration to CAPs that have identity set to "' AP_WORK_* " and we are going to assign the Config_GUEST configuration to CAPs that have identity set to " AP_GUEST_* ". To do this, you simply need to change the CAPsMAN provisioning rules. 

Remove any existing provisioning rules 

```
/caps-man provisioning remove [f]
```

Create new provisioning rules that will assign appropriate configuration on a CAP based on its identity 

```
/caps-man provisioning
add action=create-dynamic-enabled identity-regexp=^AP_GUEST_ master-configuration=Config_GUEST
add action=create-dynamic-enabled identity-regexp=^AP_WORK_ master-configuration=Config_WORK
```

**==> picture [13 x 13] intentionally omitted <==**

Don't forget to set a proper identity on the CAPs since CAPsMAN is going to assign appropriate configuration on the APs based on it's identity. 

1549
