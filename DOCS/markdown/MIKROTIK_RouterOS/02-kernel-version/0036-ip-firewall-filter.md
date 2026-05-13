## `/ip firewall filter` 

```
  add chain=input action=accept connection-state=established,related,untracked comment="accept established,
related,untracked"
```

```
  add chain=input action=drop connection-state=invalid comment="drop invalid"
```

```
  add chain=input in-interface=ether1 action=accept protocol=icmp comment="accept ICMP"
```

```
  add chain=input in-interface=ether1 action=accept protocol=tcp port=8291 comment="allow Winbox";
  add chain=input in-interface=ether1 action=accept protocol=tcp port=22 comment="allow SSH";
  add chain=input in-interface=ether1 action=drop comment="block everything else";
```

**==> picture [13 x 13] intentionally omitted <==**

If the public interface is PPPoE, LTE, or any other type, the 'in-interface' should be set to that interface. 

The first rule accepts packets from already established connections, assuming they are safe to not overload the CPU. The second rule drops any packet that connection tracking identifies as invalid. After that, we set up typical accept rules for specific protocols. 

If you are using Winbox/WebFig for configuration, here is an example of how to add an established/related/untracked rule: 

- Open the IP -> Firewall window and navigate to the Filter Rules tab; Click on the "+" button to open a new dialog; 

- Select " input " for the chain. 

- Click on " Connection state " and check the boxes for " established ," " related ," and " untracked ." Go to the Action tab and ensure that " accept " is selected. Click on OK to apply the settings. 

28 

**==> picture [505 x 247] intentionally omitted <==**

**==> picture [505 x 259] intentionally omitted <==**

To add additional rules, click on the "+" button for each new rule and fill in the same parameters as provided in the console example.
