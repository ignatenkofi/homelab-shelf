## /routing/rpki 

**==> picture [506 x 265] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IPv4/6) mandatory Address of the RTR server<br>disabled (yes | no; Default: no ) Whether the item is ignored.<br>expire-interval  (integer [600..172800];  Time interval [s] polled data is considered valid in the absence of a valid subsequent update from the<br>Default: 7200) validator.<br>group  (string) mandatory Name of the group a database is assigned to.<br>port  (integer [0..65535]; Default: 323) Connection port number<br>preference  (integer [0..4294967295];  If there are multiple RTR sources, the preference number indicates a more preferred one. A higher<br>Default: 0) number is preferred.<br>If preference is not configured then lowest remote IP within a group is preferred, if IPs are equal then<br>lowest remote port is preferred.<br>refresh-interval  (integer [1..86400];  Time interval [s] to poll the newest data from the validator.<br>Default: 3600)<br>retry-interval  (integer [1..7200]; Default:  Time Interval [s] to retry after the failed data poll from the validator.<br>600)<br>vrf (name; Default: main) Name of the VRF table used to bind the connection to.<br>**----- End of picture text -----**<br>

986
