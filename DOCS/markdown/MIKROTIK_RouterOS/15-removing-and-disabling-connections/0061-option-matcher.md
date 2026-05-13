## Option matcher 

The Option matcher allows to identify DHCP clients by any of DHCP options and assign IP address from specific IP pool. 

It is possible to perform `exact` (provided value should match exactly ) or `substring` matching (will look for value match anywhere in the option string — it can match values at the start, middle, or end). 

Substring matching is useful in cases where value can change depending on the end device, for example, if the class-identifier sent by the device contains not only vendor information, but also exact MAC or other additional information. 

**==> picture [13 x 13] intentionally omitted <==**

It's possible to define two substring matches for the same option, for example, one that matches "ABC" and another one that matches "ABCDE", if there is a DHCP option with the value of "ABCDEF", both entries would match it, but the matcher that will get applied will be selected randomly. 

**==> picture [13 x 13] intentionally omitted <==**

Clients with a static lease will continue to receive their static address, even when matched by the option matcher.
