## `/routing/pimsm/interface-template` 

The interface template menu defines which interfaces will participate in PIM and what per-interface configuration will be used. 

**==> picture [516 x 114] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>hello-delay  ( Randomized interval for the initial Hello message on interface startup or detecting new neighbor.<br>time;<br>Default: 5s )<br>hello-period Periodic interval for Hello messages.<br>(time;<br>Default:  30s<br>)<br>**----- End of picture text -----**<br>

975 

**==> picture [516 x 395] intentionally omitted <==**

**----- Start of picture text -----**<br>
instance  (n Name of the PIM instance this interface template belongs to.<br>ame;<br>Default: )<br>interfaces  ( List of interfaces that will participate in PIM.<br>name;<br>Default: all )<br>join-prune-<br>period  (time<br>; Default:  1m<br>)<br>join- Sets the value of a Tracking (T) bit in the LAN Prune Delay option in the Hello message. When enabled, a router advertises its willingness<br>tracking- to disable Join suppression. it is possible for upstream routers to explicitly track the join membership of individual downstream routers if<br>support  (ye Join suppression is disabled. Unless all PIM routers on a link negotiate this capability, explicit tracking and the disabling of the Join<br>s | no;  suppression mechanism are not possible.<br>Default: yes )<br>override- Sets the maximum time period over which to randomize when scheduling a delayed override Join message on a network that has join<br>interval  (time suppression enabled.<br>; Default:  2<br>s500ms )<br>priority  (inte The Designated Router (DR) priority. A single Designated Router is elected on each network. The priority is used only if all neighbors<br>ger: 0.. have advertised a priority option. Numerically largest priority is preferred. In case of a tie or if priority is not used - the numerically largest<br>4294967295 IP address is preferred.<br>; Default:  1 )<br>propagation Sets the value for a prune pending timer. It is used by upstream routers to figure out how long they should wait for a Join override<br>-delay  (time message before pruning an interface that has join suppression enabled.<br>; Default:  5<br>00ms )<br>source-<br>addresses (<br>IPv4 | IPv6;<br>Default: )<br>**----- End of picture text -----**<br>
