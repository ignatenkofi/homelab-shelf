## Strip netmask 

This script is useful if you need an IP address without a netmask (for example to use it in a firewall), but " `/ip address get [id] address` " returns the IP address and netmask. 

```
:global ipaddress 10.1.101.1/24
:for i from=( [:len $ipaddress] - 1) to=0 do={
        :if ( [:pick $ipaddress $i] = "/") do={
                :put [:pick $ipaddress 0 $i]
        }
}
```

Another much more simple way: 

```
:global ipaddress 10.1.101.1/24
:put [:pick $ipaddress 0 [:find $ipaddress "/"]]
```
