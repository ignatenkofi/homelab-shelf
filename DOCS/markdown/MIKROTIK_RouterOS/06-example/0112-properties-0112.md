## Properties 

323 

**==> picture [516 x 219] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP/mask | IPv6 prefix;  Host or network address from which the user is allowed to log in<br>Default: )<br>group  (string; Default: ) Name of the group the user belongs to<br>inactivity-policy  (lockscreen | logout  Specifies inactivity action - logout (user will be logged out) or lockscreen (session will be locked, require password<br>| none; Default: none ) input to continue). Works only for CLI sessions.<br>inactivity-timeout  (time; Default: 10 Specifies time after which user will be logged out or session will be locked. Minimal timeout - 1 minute, maximal<br>min ) timeout - 24 hours. Works only for CLI sessions.<br>name  (string; Default: ) User name. Must start and end with an alphanumeric character but can include "_", ".", "#", "-", and "@" symbols.<br>However the "*" symbol is prohibited in the user name.<br>password  (string; Default: ) User password. If not specified, it is left blank (hit [Enter] when logging in). It conforms to standard Unix<br>characteristics of passwords and may contain letters, digits, "*" and "_" symbols.<br>last-logged-in  (time and date;  Read-only field. Last time and date when a user logged in.<br>Default: ) ""<br>**----- End of picture text -----**<br>
