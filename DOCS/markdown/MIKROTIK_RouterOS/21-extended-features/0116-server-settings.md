## Server settings 

**==> picture [516 x 131] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>comment  (string; Default:  Mi Set comment for the server<br>krotikSMB )<br>domain  (string; Default:  MS Name of Windows Workgroup<br>HOME )<br>enabled  (yes | no | auto Def The default value is 'auto.' This means that the SMB server will automatically be enabled when the first non-disabled<br>ault:  auto ) SMB share is configured under '/ip smb share'<br>interface  (string; Default:  all ) List of interfaces on which SMB service will be running. all - SMB will be available on all interfaces.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

Starting from version 7.14, the 'allow-guest' option has been replaced by a default guest user located in 'ip/smb/users'. This default guest user can now be disabled or enabled in this section.
