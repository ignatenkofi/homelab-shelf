## /routing/id 

Global Router ID election configuration. ID can be configured explicitly or set to be elected from one of the Routers IP addresses. 

For each VRF table RouterOS adds dynamic ID instance, that elects the ID from one of the IP addresses belonging to a particular VRF: 

```
[admin@rack1_b33_CCR1036] /routing/id> print
Flags: D - DYNAMIC, I - INACTIVE
Columns: NAME, DYNAMIC-ID, SELECT-DYNAMIC-ID, SELECT-FROM-VRF
#   NAME   DYNAMIC-ID      SELECT-D   SELE
0 D main   111.111.111.2   only-vrf   main
```

**==> picture [516 x 332] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>comment  (string)<br>disabled  (yes | no) ID reference is not used.<br>id (IP) Parameter to explicitly set the Router ID. If ID is not explicitly specified, then it can be elected from one of<br>the configured IP addresses on the router. See parameters select-dynamic-id and select-from-vrf.<br>name  (string) Reference name<br>select-dynamic-id (any | lowest | only- States what IP addresses to use for the ID election:<br>active | only-loopback | only-static | only-<br>vrf) any - any address found on the router can be elected as the Router ID.<br>lowest - pick the lowest IP address.<br>only-active - pick an ID only from active IP addresses.<br>only-loopback - pick an ID only from loopback addresses (loopback address is considered any non<br>point to point /32 address).<br>only-vrf - pick an ID only from selected VRF. Works with select-from-vrf property.<br>select-from-vrf  (name) VRF from which to select IP addresses for the ID election.<br>Read-only Property Description<br>dynamic  (yes | no)<br>dynamic-id  (IP) Currently selected ID.<br>inactive  (yes | no) If there was a problem to get a valid ID, then item can become inactive.<br>**----- End of picture text -----**<br>


965
