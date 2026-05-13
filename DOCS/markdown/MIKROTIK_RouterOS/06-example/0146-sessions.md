## Sessions 

Sub-menu: `/user-manager session` 

Sessions are logged only if accounting is enabled on NAS. 

Read-only properties 

**==> picture [516 x 420] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>acct-session-id  ( Unique identification of the accounting session.<br>string)<br>active  (yes | no) Whether the session is currently used.<br>calling-station-id User's identifier, usually IP address or MAC address.<br>(string)<br>download  (Bytes) Amount of traffic downloaded.<br>ended  (datetime) Date and time when the session was closed. Empty for active sessions.<br>last-accounting- Date and time when the last accounting update was received.<br>packet  (datetime)<br>nas-ip-address  (I The IP address of the NAS.<br>P address)<br>nas-port-id  (string Identifier of the NAS port that is authenticating the user.<br>)<br>nas-port-type  (str The port type (physical or virtual) that is authenticating the user.<br>ing)<br>started  (datetime) Date and time when the session was established.<br>status  (list of  Possible available statuses of a session: start - accounting message Start has been received, stop - accounting message Stop has<br>statuses) been received, interim - Interim update has been received, close-acked - session is successfully closed, expired.<br>terminate-cause The reason why the session was closed.<br>(string)<br>upload  (Bytes) Amount of traffic uploaded.<br>uptime  (time) Total logged uptime on the session.<br>user  (string) Name of the user.<br>user-address  (IP  IP address provided to the user.<br>address)<br>**----- End of picture text -----**<br>
