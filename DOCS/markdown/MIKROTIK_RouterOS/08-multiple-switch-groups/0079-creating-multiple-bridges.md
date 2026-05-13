## Creating multiple bridges 

The devices support only one hardware bridge. If there are multiple bridges created, only one gets hardware offloading. While for L2 that means software forwarding for other bridges, in the case of L3HW, multiple bridges may lead to undefined behavior. 

**==> picture [13 x 13] intentionally omitted <==**

Instead of creating multiple bridges, create one and segregate L2 networks with VLAN filtering.
