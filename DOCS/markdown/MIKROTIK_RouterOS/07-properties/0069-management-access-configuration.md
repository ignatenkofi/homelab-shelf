## Management access configuration 

There are multiple ways to set up management access on a device that uses bridge VLAN filtering. Below are some of the most popular approaches to properly enable access to a router/switch. Start by creating a bridge without VLAN filtering enabled: 

```
/interface bridge
add name=bridge1 vlan-filtering=no
```
