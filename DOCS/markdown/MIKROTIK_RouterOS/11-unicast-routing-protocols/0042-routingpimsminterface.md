## `/routing/pimsm/interface` 

The interface menu shows all interfaces that are currently participating in PIM and their statuses. This menu contains dynamic and read-only entries that get created by defined interface templates. 

**==> picture [501 x 193] intentionally omitted <==**

**----- Start of picture text -----**<br>
Read-only Property Description<br>address  (IP%interface@vrf) Shows IP address, interface, and VRF.<br>designated-router  (yes | no)<br>dr  (yes | no)<br>dynamic  (yes | no)<br>instance  (name) Name of the PIM instance this interface template belongs to.<br>join-tracking  (yes | no)<br>override-interval  (time)<br>priority  (integer: 0..4294967295)<br>propagation-delay  (time)<br>**----- End of picture text -----**<br>

```
/routing/pimsm/neighbor
```

976 

The neighbor menu shows all detected neighbors that are running PIM and their statuses. This menu contains dynamic and read-only entries. 

**==> picture [516 x 205] intentionally omitted <==**

**----- Start of picture text -----**<br>
Read-only Property Description<br>address  (IP%interface) Shows the neighbor's IP address and local interface the neighbor is detected on.<br>designated-router  (yes  Shows whether the neighbor is elected as Designated Router (DR).<br>| no)<br>instance  (name) Name of the PIM instance this neighbor is detected on.<br>join-tracking  (yes | no) Indicates the neighbor's value of a Tracking (T) bit in the LAN Prune Delay option in the Hello message.<br>override-interval  (time) Indicates the neighbor's value of the override interval in the LAN Prune Delay option in the Hello message.<br>priority  (integer: 0.. Indicates the neighbor's priority value.<br>4294967295)<br>propagation-delay  (time) Indicates the neighbor's value of the propagation delay in the LAN Prune Delay option in the Hello message.<br>timeout (time) Shows the reminding time after the neighbor is removed from the list if no new Hello message is received. The hold time<br>equals to neighbor's  hello-period  * 3.5.<br>**----- End of picture text -----**<br>
