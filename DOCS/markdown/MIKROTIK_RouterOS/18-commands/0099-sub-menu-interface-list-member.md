## Sub-menu: `/interface list member` 

This sub-menu contains information about statically configured interface members to each interface list. Note that dynamically added interfaces by include and exclude statements are not represented in this sub-menu. 

**==> picture [516 x 72] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>interface  ( Name of the interface<br>string)<br>list  (string) Name of the interface list<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Care must be taken when working with bridges and lists. Adding a bridge as a member is not the same as adding all its ports! And adding all slave ports as members is not the same as adding the bridge itself. This can particularly impact functionality of neighbor discovery. 

1146 

1147
