## Properties 

**==> picture [504 x 187] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>alert-timeout  (none | time;  Time after which the alert will be forgotten. If after that time the same server is detected, a new alert will be generated.<br>Default: 1h) If set to none timeout will never expire.<br>interface  (string; Default: ) Interface, on which to run rogue DHCP server finder.<br>on-alert  (string; Default: ) Script to run, when an unknown DHCP server is detected.<br>valid-server  (string; Default: List of MAC addresses of valid DHCP servers.<br>)<br>Read-only properties<br>Property Description<br>unknown-server  (string) List of MAC addresses of detected unknown DHCP servers. The server is removed from this list after alert-timeout<br>**----- End of picture text -----**<br>


Read-only properties 

Menu specific commands 

**==> picture [164 x 43] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>reset-alert  (id) Clear all alerts on an interface<br>**----- End of picture text -----**<br>
