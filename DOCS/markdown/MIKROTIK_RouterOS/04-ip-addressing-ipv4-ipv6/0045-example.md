## Example 

To define a pool named "my-pool" with the 10.0.0.1-10.0.0.126 address range excluding gateway's address 10.0.0.1 and server's address 10.0.0.100, and the other pool dhcp-pool, with the 10.0.0.200-10.0.0.250 address range: 

```
[admin@MikroTik] ip pool> add name=my-pool ranges=10.0.0.2-10.0.0.99,10.0.0.101-10.0.0.126
[admin@MikroTik] ip pool> add name=dhcp-pool ranges=10.0.0.200-10.0.0.250
[admin@MikroTik] ip pool> print
  # NAME                                        RANGES
  0 ip-pool                                     10.0.0.2-10.0.0.99
                                                10.0.0.101-10.0.0.126
  1 dhcp-pool                                   10.0.0.200-10.0.0.250
```
