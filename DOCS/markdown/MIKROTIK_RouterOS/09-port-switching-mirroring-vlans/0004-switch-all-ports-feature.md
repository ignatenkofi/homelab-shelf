## Switch All Ports Feature 

Ether1 port on RB450G/RB435G/RB850Gx2 devices has a feature that allows it to be removed/added to the default switch group, this setting is available on the `/interface ethernet switch` menu. By default ether1 port will be included in the switch group. 

**==> picture [504 x 204] intentionally omitted <==**

**==> picture [516 x 102] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>switch-all-ports  (no |  Changes ether1 switch group only on RB450G/RB435G/RB850Gx2 devices.<br>yes; Default:  yes )<br>yes  - ether1 is part of the switch and supports switch grouping and all other advanced Atheros8316/Atheros8327 features<br>including extended statistics ( /interface ethernet print stats ).<br>no  - ether1 is not part of the switch, effectively making it a stand-alone ethernet port, this way increasing its throughput to<br>other ports in bridged and routed mode, but removing the switching possibility on this port.<br>**----- End of picture text -----**<br>
