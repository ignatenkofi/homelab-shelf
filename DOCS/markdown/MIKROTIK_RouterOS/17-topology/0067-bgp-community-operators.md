## BGP Community Operators 

**==> picture [500 x 118] intentionally omitted <==**

**----- Start of picture text -----**<br>
Operator Description Example<br>equal return true if provided communities are equal to the routes property value<br>equal-list return true if communities from provided community-list are equal to the route's property value<br>any returns true if the route's property value contains at least one of provided communities<br>any-list returns true if the route's property value contains at least one community from the provided list<br>includes returns true if the route's property value includes specified communities<br>**----- End of picture text -----**<br>


1059 

**==> picture [500 x 95] intentionally omitted <==**

**----- Start of picture text -----**<br>
includes-list returns true if the route's property value includes all communities from the specified communities-list<br>subset returns true if route community subset matches communities from the list 1:1,3:3 will match 1:1,2:2,3:3<br>subset-list the same as "subset", but matches communities form the community list.<br>any-regexp the same as "any", but matched by regexp<br>subset-regexp the same as "subset", but matched by regexp<br>**----- End of picture text -----**<br>
