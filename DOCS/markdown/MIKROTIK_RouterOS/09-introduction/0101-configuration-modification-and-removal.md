## Configuration modification and removal 

In certain situations, CB and PE device configuration needs to be adjusted (e.g. PE device needs new control ports) or removed completely. To modify the PE device configuration, all related PE device configuration should be removed from the CB device first. Only then the new configuration can be applied. 

549 

First, to remove PE configuration from CB, disable the PE using the following command: 

```
/interface bridge port-extender set switch=none control-ports="" excluded-ports=""
```

Then, on the CB device, remove the related bridge and other RouterOS configuration where PE interfaces were used (e.g. see the export from " `/inte rface bridge port` " and " `/interface bridge vlan` " menus). For example, to remove all bridge ports from a specific PE device, use the command below: 

```
/interface bridge port remove [find interface~"pe1"]
```

Once the configuration is removed, PE can be removed from the CB device list. This command will also automatically remove all the PE device interfaces from the CB interface list. In case some PE interface configuration is still applied on the CB, it will not be valid anymore. Use `print` command to find out the PE device name. 

```
/interface bridge port-controller device remove [find name=pe1]
```

550
