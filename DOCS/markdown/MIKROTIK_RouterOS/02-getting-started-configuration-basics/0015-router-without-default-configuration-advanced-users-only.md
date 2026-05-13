## Router without Default Configuration (advanced users only) 

If the router doesn't have a default configuration, there are multiple options to consider. However, in this case, we'll opt for a method that best fits our requirements. Connect the ISP cable to the router's ether1 port and connect your PC to any port except ether1. Then, launch WinBox and search for your router using the neighbor discovery feature. See detailed example in Winbox article. If the router appears in the list, select its MAC address and click Conne ct . 

The easiest method to ensure a completely clean router is to run the CLI command 

```
/system reset-configuration no-defaults=yes skip-backup=yes
```
