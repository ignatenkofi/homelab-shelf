## Configuration Explained 

First, we will send every new connection to the specific firewall chain where we will detect DDoS: 

```
/ip/firewall/filter/add chain=forward connection-state=new action=jump jump-target=detect-ddos
```

742 

In the newly created chain, we will add the following rule with the "dst-limit" parameter. This parameter is written in the following format: dst-limit=count[ /time],burst,mode[/expire] . We will match 32 packets with 32 packet burst based on destination and source address flow, which renews every 10 seconds. The rule will work until a given rate is exceeded. 

```
/ip/firewall/filter/add chain=detect-ddos dst-limit=32,32,src-and-dst-addresses/10s action=return
```

So far all the legitimate traffic should go through the "action=return", but in the case of DoS/DDoS "dst-limit" buffer will be fulfilled and a rule will not "catch" any new traffic. Here come the next rules, which will deal with the attack. Let`s start with creating a list for attackers and victims which we will drop: 

```
ip/firewall/address-list/add list=ddos-attackers
```

```
ip/firewall/address-list/add list=ddos-targets
```

```
ip/firewall/raw/add chain=prerouting action=drop src-address-list=ddos-attackers dst-address-list=ddos-targets
```

With the firewall filter section, we will add attackers in the "DDoS-attackers" and victims in list "ddos-targets" list:
