## MAC Connectivity Access 

By default, the MAC server runs on all interfaces. To restrict MAC connectivity from the WAN port, we'll disable the default all entry and add a LAN interface. 

First, create an interface list: 

```
[admin@MikroTik] > /interface list add name=LAN
```

25 

**==> picture [376 x 404] intentionally omitted <==**

Then, add your previously created bridge named "bridge1" to the interface list: 

```
[admin@MikroTik] > /interface list member add list=LAN interface=bridge1
```

26 

**==> picture [226 x 272] intentionally omitted <==**

Apply newly created interface list to the MAC server: 

```
[admin@MikroTik] > /tool mac-server set allowed-interface-list=LAN
```

**==> picture [451 x 212] intentionally omitted <==**

Do the same for Winbox MAC access 

```
[admin@MikroTik] > /tool mac-server mac-winbox set allowed-interface-list=LAN
```

Winbox/Webfig actions: 

Navigate to Interfaces → Interface List → Lists window; Click on the "+" button to add a new list; 

- Enter " LAN " into the Name field and click OK ; Return to the Interfaces → Interface List section; Click on the "+" button; 

27 

Select " LAN " from the dropdown List options; 

- Choose " bridge1 " from the dropdown Interface options; Click OK to confirm; 

- Open Tools -> Mac Server window; 

Click on the MAC Telnet Server button; 

In the new dialog, select the newly created list " LAN " from the dropdown list; Click OK to apply settings. 

Do the same in the MAC Winbox Server tab to block Mac Winbox connections from the internet.
