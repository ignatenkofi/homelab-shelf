## Host Table 

485 

The host table represents switch chip's internal MAC address to port mapping. It can contain two kinds of entries: dynamic and static. Dynamic entries get added automatically, this is also called a learning process: when switch chip receives a packet from a certain port, it adds the packet's source MAC address and port it received the packet from to the host table, so when a packet comes in with the same destination MAC address, it knows to which port it should forward the packet. If the destination MAC address is not present in the host table (so-called unknown-unicast traffic) then it forwards the packet to all ports in the group. Dynamic entries take about 5 minutes to time out. Learning is enabled only on ports that are configured as part of the switch group, so you won't see dynamic entries if you have not set up port switching. Also, you can add static entries that take over dynamic if a dynamic entry with the same MAC address already exists. Since port switching is configured using a bridge with hardware offloading, any static entries created on one table (either bridge host or switch host) will appear on the opposite table as a dynamic entry. Adding a static entry on the switch host table will provide access to some more functionality that is controlled via the following params: 

**==> picture [516 x 288] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>copy-to-cpu  (no | yes;  Whether to send a frame copy to switch CPU port from a frame with a matching MAC destination address (matching<br>Default: no ) destination or source address for CRS3xx series switches)<br>drop  (no | yes; Default: Whether to drop a frame with a matching MAC source address received on a certain port (matching destination or source<br>no ) address for CRS3xx series switches)<br>mac-address  (MAC; Def Host's MAC address<br>ault: 00:00:00:00:00:00 )<br>mirror  (no | yes; Default: Whether to send a frame copy to  mirror-target  port from a frame with a matching MAC destination address (matching<br>no ) destination or source address for CRS3xx series switches)<br>ports  (name; Default: no Name of the interface, static MAC address can be mapped to more than one port, including switch CPU port<br>ne )<br>redirect-to-cpu  (no | yes Whether to redirect a frame to switch CPU port from a frame with a matching MAC destination address (matching destination<br>; Default: no ) or source address for CRS3xx series switches)<br>share-vlan-learned  (no | Whether the static host MAC address lookup is used with shared-VLAN-learning (SVL) or independent-VLAN-learning (IVL).<br>yes; Default: no ) The SVL mode is used for those VLAN entries that do not support IVL or IVL is disabled (independent-learning=no)<br>switch  (name; Default: n Name of the switch to which the MAC address is going to be assigned to<br>one )<br>vlan-id  (integer: 0..4095; VLAN ID for the statically added MAC address entry<br>Default: )<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

Every switch chip has a finite number of MAC addresses it can store on the chip, see the Introduction table for a specific host table size. Once a host table is full, different techniques can be utilized to cope with the situation, for example, the switch can remove older entries to free space for more recent MAC addresses (used on QCA-8337 and Atheros-8327 switch chips), another option is to simply ignore the new MAC addresses and only remove entries after a timeout has passed (used on Atheros8316, Atheros8227, Atheros-7240, ICPlus175D and Realtek-RTL8367 switch chips), the last option is a combination of the previous two - only allow a certain amount of entries to be renewed and keep the other host portion intact till the timeout (used on MediaTek-MT7621, MT7531, EN7523 switch chip). These techniques cannot be changed with configuration. 

**==> picture [13 x 13] intentionally omitted <==**

For Atheros8316, Atheros8227 and Atheros-7240 switch chips, the switch-cpu port will always participate in the host learning process when at least one hardware offloaded bridge port is active on the switching group. It will cause the switch-cpu port to learn MAC addresses from nonHW offloaded interfaces. This might cause packet loss when a single bridge contains HW and non-HW offloaded interfaces. Also, packet loss might appear when a duplicate MAC address is used on the same switching group regardless if hosts are located on different logical networks. It is recommended to use HW offloading only when all bridge ports can use HW offloaded or keep it disabled on all switch ports when one or more bridge ports cannot be configured with HW offloading. 

486 

**==> picture [13 x 13] intentionally omitted <==**

The switch chips QCA-8337 and Atheros-8327 automatically add reserved mulitcast MAC addresses (01:80:C2:00:00:0x) to the host table when hardware-offloaded bridge is created with forward-reserved-addresses=no and protocol-mode=stp/rstp . These MACs should not be forwarded by 802.1Q compatible bridges and they are essential for correct operation with R/STP. Since the switch has a limited number of host table entries, these MAC addresses are only assigned to VLAN 1. 

To ensure packets with these destination MAC addresses are processed correctly: 

Switch ports should be set to default VLAN 1 ( `default-vlan-id=auto` or `default-vlan-id=1` ). If VLAN 1 is explicitly configured, it must use independent VLAN learning ( `independent-learning=yes` ).
