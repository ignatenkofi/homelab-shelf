## Chains 

Firewall filtering rules are grouped together in chains. It allows a packet to be matched against one common criterion in one chain, and then passed over for processing against some other common criteria to another chain. 

636 

For example, a packet should be matched against the IP address:port pair. Of course, it could be achieved by adding as many rules with IP address:port match as required to the forward chain, but a better way could be to add one rule that matches traffic from a particular IP address. Then rules that perform matching against separate ports can be added to " mychain " chain without specifying the IP addresses. 

```
/ip firewall filter
```

```
add chain=mychain protocol=tcp dst-port=22 action=accept
add chain=mychain protocol=tcp dst-port=23 action=accept
```

```
add chain=input src-address=1.1.1.2/32 jump-target="mychain"
```

When processing a chain, rules are taken from the chain in the order they are listed, from top to bottom. If a packet matches the criteria of the rule, then the specified action is performed on it, and no more rules are processed in that chain (the exception is the passthrough action and some Mangle actions). 

If a packet has not matched any rule within the chain, then it is accepted. 

Each firewall module has its own pre-defined chains: 

**==> picture [68 x 164] intentionally omitted <==**

**----- Start of picture text -----**<br>
raw :<br>prerouting<br>output<br>filter<br>input<br>forward<br>output<br>mangle<br>prerouting<br>input<br>forward<br>output<br>postrouting<br>nat<br>srcnat<br>dstnat<br>**----- End of picture text -----**<br>


More detailed packet processing in RouterOS is described in the Packet Flow in the RouterOS diagram. 

637
