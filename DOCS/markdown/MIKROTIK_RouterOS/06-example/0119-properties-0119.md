## Properties 

**==> picture [516 x 213] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>accounting  (yes | no;  If the RADIUS server should be sent accounting of login, logout. Bandwidth usage statistics are not part of  /user<br>Default:  yes ) accounting<br>exclude-groups  (list of  Exclude-groups consist of the groups that should not be allowed to be used for users authenticated by radius. If the radius<br>group names; Default: ) server provides a group specified in this list, the default-group will be used instead.<br>This is to protect against privilege escalation when one user (without policy permission) can change the radius server list,<br>set up its own radius server and<br>log in as admin.<br>default-group  (string;  User group used by default for users authenticated via a RADIUS server.<br>Default:  read )<br>interim-update  (time;  Interim-Update time interval<br>Default:  0s )<br>use-radius  (yes |no;  Enable user authentication via RADIUS<br>Default:  no )<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

If you are using RADIUS, you need to have CHAP support enabled in the RADIUS server for WinBox to work
