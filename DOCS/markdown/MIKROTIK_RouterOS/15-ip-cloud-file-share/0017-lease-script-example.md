## Lease script example 

It is possible to execute a script when a DHCP client obtains a new lease or loses an existing one. This is an example script that automatically adds a default route with routing-table=WAN1 and removes it when the lease expires or is removed. 

**==> picture [13 x 13] intentionally omitted <==**

Be aware that some variables might be reserved in specific menus and cannot be used there. More info find here. 

886 

```
/ip dhcp-client
add add-default-route=no dhcp-options=hostname,clientid disabled=no interface=ether2 script="{\r\
    \n    :local rmark \"WAN1\"\r\
    \n    :local count [/ip route print count-only where comment=\"WAN1\"]\r\
    \n    :if (\$bound=1) do={\r\
    \n        :if (\$count = 0) do={\r\
    \n            /ip route add gateway=\$\"gateway-address\" comment=\"WAN1\" routing-table=\$rmark\r\
    \n        } else={\r\
    \n            :if (\$count = 1) do={\r\
    \n                :local test [/ip route find where comment=\"WAN1\"]\r\
    \n                :if ([/ip route get \$test gateway] != \$\"gateway-address\") do={\r\
    \n                    /ip route set \$test gateway=\$\"gateway-address\"\r\
    \n                }\r\
    \n            } else={\r\
    \n                :error \"Multiple routes found\"\r\
    \n            }\r\
    \n        }\r\
    \n    } else={\r\
    \n        /ip route remove [find comment=\"WAN1\"]\r\
    \n    }\r\
    \n}\r\
    \n"
```
