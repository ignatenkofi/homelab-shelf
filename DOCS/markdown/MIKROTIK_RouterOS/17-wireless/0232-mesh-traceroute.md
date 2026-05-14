## Mesh traceroute 

There is also a mesh traceroute command, that can help you to determine which paths are used for routing. 

For example, for this network: 

```
[admin@1] /interface mesh fdb print
Flags: A - active, R - root
MESH TYPE MAC-ADDRESS ON-INTERFACE LIFETIME AGE
A mesh1 local 00:0C:42:00:00:01 7m1s
A mesh1 mesh 00:0C:42:00:00:02 wds4 17s 4s
A mesh1 mesh 00:0C:42:00:00:12 wds4 4m58s 1s
A mesh1 mesh 00:0C:42:00:00:13 wds4 19s 2s
A mesh1 neighbor 00:0C:42:00:00:16 wds4 7m1s
A mesh1 mesh 00:0C:42:00:00:24 wds4 18s 3s
```
