## Resolve default gateway when 'router' (option3) is from a different subnet 

In some cases, administrators tend to set the 'router' option which cannot be resolved with offered IP's subnet. For example, the DHCP server offers 192.168.88.100/24 to the client, and option 3 is set to 172.16.1.1. This will result in an unresolved default route: 

```
 #      DST-ADDRESS        PREF-SRC        GATEWAY            DISTANCE
 0  DS  0.0.0.0/0                          172.16.1.1              1
 1 ADC  192.168.88.0/24    192.168.88.100  ether1
```

To fix this we need to add /32 route to resolve the gateway over ether1, which can be done by the running script below each time the DHCP client gets an address 

```
/system script add name="dhcpL" source={ /ip address add address=($"lease-address" . "/32") network=$"gateway-
address" interface=$interface }
```

Now we can further extend the script, to check if the address already exists, and remove the old one if changes are needed 

887 

```
/system script add name="dhcpL" source={
  /ip address {
    :local ipId [find where comment="dhcpL address"]
    :if ($ipId != "") do={
      :if (!([get $ipId address] = ($"lease-address" . "/32") && [get $ipId network]=$"gateway-address" )) do={
        remove $ipId;
        add address=($"lease-address" . "/32") network=$"gateway-address" \
          interface=$interface comment="dhcpL address"
      }
    } else={
      add address=($"lease-address" . "/32") network=$"gateway-address" \
        interface=$interface comment="dhcpL address"
    }
  }
}
```
