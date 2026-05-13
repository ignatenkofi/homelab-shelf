## Sub-menu: `/interface list` 

This menu contains information about all interface lists available on the router. There are four predefined lists - `all` (contains all interfaces), `none` (contain s no interfaces), `dynamic` (contains dynamic interfaces), and `static` (contains static interfaces). It is also possible to create additional interface lists. 

**==> picture [13 x 12] intentionally omitted <==**

Dynamic interfaces are interfaces that have a "dynamic" flag. Any interface that doesn't have a dynamic flag will be part of the `static` interface list. 

Property Description name (string) Name of the interface list include (string) Defines interface list which members are included in the list. It is possible to add multiple lists separated by commas exclude (string) Defines interface list which members are excluded from the list. It is possible to add multiple lists separated by commas 

Members are added to the interface list in the following order: 

1.  include members are added to the interface list 

2.  exclude members are removed from the list 

3.  Statically configured members are added to the list
