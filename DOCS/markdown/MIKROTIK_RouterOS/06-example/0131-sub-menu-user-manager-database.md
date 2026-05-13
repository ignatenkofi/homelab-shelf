## Sub-menu: `/user-manager database` 

All RADIUS-related information is stored in a separate User Manager's database configurable under the "database" sub-menu. "Enabled" and "db-path" are the only parameters that are not stored in the User Manager's database and instead are stored in the main RouterOS configuration table meaning that these parameters will be affected by the RouterOS configuration reset. The rest of the configuration, session, and payment data is stored in a separate SQLite database on the FLASH storage of the device. When performing any actions with databases, it is advised to make a backup before and after any activity. 

Properties 

333 

|Property|Description|
|---|---|
|db-path(<br>; Default: )<br>string|Path to the location where database files will be stored.|
|Read-only properties||



**==> picture [270 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>db-size The current size of the database.<br>free-disk-space Free space left on the disk where the database is stored.<br>**----- End of picture text -----**<br>
