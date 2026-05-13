## Sub-menu: `/ip smb shares` 

Allows configuring share names and directories that will be accessible by SMB. 

If the directory provided in the configuration does not exist it will be created automatically. 

**==> picture [516 x 189] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>comment  (string;  Set a comment for the share<br>Default:  default share )<br>disabled  (yes | no;  If disabled, the share will not be accessible.<br>Default:  no )<br>valid-users  (list of strings Specifies which users are allowed to access the Samba share. If it is left empty, all users will be able to access the share,<br>; | Default:) once user or users are defined here, only they will be able to access the share<br>invalid-users  (list of strin Used to specify users who are explicitly denied access to the Samba share.<br>gs; | Default: )<br>require-encryption  (yes  | Enforces the use of encryption for all connections to a particular Samba share. It is recommended to change this to "Yes" to<br>no; Default: no ) ensure better stability with macOS clients.<br>name  (string; Default: ) Name of the SMB share<br>**----- End of picture text -----**<br>


1898 

directory (string; Default: ) 

Directory on router assigned to SMB share. If left empty value of the name argument will be used from the root folder.
