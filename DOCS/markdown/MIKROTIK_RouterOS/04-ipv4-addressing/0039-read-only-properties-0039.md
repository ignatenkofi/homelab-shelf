## Read-only Properties 

**==> picture [506 x 333] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (ipv6 address) IPv6 address of the node.<br>interface  (string) The interface on which the node was detected.<br>mac-address  (string) Mac address of the discovered node.<br>router  (yes | no) Whether the discovered node is a router<br>status  (noarp | incomplete |  Status of the cached entry:<br>stale | reachable | delay | probe<br>| failed) noarp  - the neighbor entry is valid. No attempts to validate this entry will be made but it can be removed<br>when its lifetime expires<br>incomplete  - address resolution is in progress and the link-layer address of the neighbor has not yet been<br>determined;<br>reachable  - the neighbor is known to have been reachable recently (within tens of seconds ago);<br>stale  - the neighbor is no longer known to be reachable but until traffic is sent to the neighbor, no attempt<br>should be made to verify its reachability;<br>delay  - the neighbor is no longer known to be reachable, and traffic has recently been sent to the neighbor,<br>probes are delayed for a short period in order to give upper layer protocol a chance to provide reachability<br>confirmation;<br>probe  - the neighbor is no longer known to be reachable, and unicast Neighbor Solicitation probes are being<br>sent to verify reachability.<br>failed  - the router was unable to resolve the neighbor’s MAC address using neighbor discovery protocol.<br>VRF  (string) Indicates which VRF this neighbor entry is associated with.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

The default maximum number of neighbor entries depends on the installed amount of RAM. It can be adjusted with the command " `/ipv6 settings set max-neighbor-entries=x` ", see more details on IPv6 Settings.
