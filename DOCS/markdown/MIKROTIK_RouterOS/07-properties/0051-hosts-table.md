## Hosts Table 

MAC addresses that have been learned on a bridge interface can be viewed in the host menu. Below is a table of parameters and flags that can be viewed. 

Sub-menu: `/interface bridge host` 

**==> picture [502 x 238] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (read-only:  The bridge the entry belongs to<br>name)<br>disabled  (read-only:  Whether the static host entry is disabled<br>flag)<br>dynamic  (read-only:  Whether the host has been dynamically created<br>flag)<br>external  (read-only:  Whether the host has been learned using an external table, for example, from a switch chip or Wireless registration table.<br>flag) Adding a static host entry on a hardware-offloaded bridge port will show no flag.<br>invalid  (read-only: flag) Whether the host entry is invalid, can appear for statically configured hosts on already removed interface<br>local  (read-only: flag) Whether the host entry is created from the bridge itself (that way all local interfaces are shown)<br>mac-address  (read- Host's MAC address<br>only: MAC address)<br>on-interface  (read- Which of the bridged interfaces the host is connected to<br>only: name)<br>**----- End of picture text -----**<br>
