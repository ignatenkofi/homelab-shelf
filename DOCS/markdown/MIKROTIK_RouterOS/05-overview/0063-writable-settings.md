## Writable Settings 

Client configuration settings. 

**==> picture [516 x 227] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled enable/disable CWMP protocol<br>acs-url URL of ACS. Examples: "https://example.com:8080/path/", "https://192.168.1.100/"<br>If ACS is accessed using HTTPS, in a client must be imported Root CA to verify ACS server certificate.<br>username HTTP authentication username (used by CPE to "login" into ACS)<br>password HTTP authentication password (used by CPE to "login" into ACS)<br>periodic- enable/disable CPE periodical session initiation. Timer is started after every successful session. When session is started by periodic<br>inform- interval then Inform RPC contains "2 PERIODIC" event. Maps to "Device.ManagementServer.PeriodicInformEnable" Parameter<br>enabled<br>periodic- timer interval of periodic inform. Maps to "Device.ManagementServer.PeriodicInformInterval"<br>inform-<br>interval<br>client- certificate of client/CPE, which can be used by ACS for extra authentication<br>certificate<br>**----- End of picture text -----**<br>


Read-only Settings 

247 

Read only parameters to monitor state of the client. 

**==> picture [516 x 231] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>status informative status of CWMP.<br>disabled - protocol disabled,<br>waiting-URL - protocol enabled, but ACS URL not configured,<br>running - CWMP is configured correctly and will communicate with ACS on events<br>last-session- user-friendly error description indicating why the previous session didn't finish successfully<br>error<br>retry-count consecutive unsuccessful session count. If > 0, then last-session-error should indicate error. Resets to 0 on a successful session,<br>disabled protocol or reboot<br>Commands<br>Command Description<br>reset-tr069- completely resets and forgets tr069-client configuration and state (without affecting other ROS configurations). Use when CWMP goes<br>config into unresponsive/hanged state and should be restored without re-installation of the RouterOS.<br>**----- End of picture text -----**<br>
