## Protecting the Clients 

Now it is time to add some protection for clients on our LAN. We will start with a basic set of rules. 

```
/ip firewall filter
```

```
  add chain=forward action=fasttrack-connection connection-state=established,related \
    comment="fast-track for established,related";
```

```
  add chain=forward action=accept connection-state=established,related \
    comment="accept established,related";
  add chain=forward action=drop connection-state=invalid
  add chain=forward action=drop connection-state=new connection-nat-state=!dstnat \
    in-interface=ether1 comment="drop access to clients behind NAT from WAN"
```

A ruleset is similar to input chain rules (accept established/related and drop invalid), except the first rule with `action=fasttrack-connection` . This rule allows established and related connections to bypass the firewall and significantly reduce CPU usage. 

Another difference is the last rule which drops all new connection attempts from the WAN port to our LAN network (unless DstNat is used). Without this rule, if an attacker knows or guesses your local subnet, he/she can establish connections directly to local hosts and cause a security threat. 

For more detailed examples on how to build firewalls will be discussed in the firewall section. 

32
