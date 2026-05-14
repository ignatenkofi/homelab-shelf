## Saving a backup 

Sub-menu: `/system backup save` 

**==> picture [506 x 141] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>dont-encrypt  (yes | no;  Disable backup file encryption. Note that since RouterOS v6.43 without a provided password, the backup file is<br>Default: no ) unencrypted.<br>encryption  (aes-sha256 | rc4;  The encryption algorithm to use for encrypting the backup file. Note that is not considered a secure encryption<br>Default: aes-sha256 ) method and is only available for compatibility reasons with older RouterOS versions.<br>name  (string; Default: [identity The filename for the backup file.<br>]-[date]-[time].backup )<br>password  (string; Default: ) Password for the encrypted backup file. Note that since RouterOS v6.43 without a provided password, the backup<br>file is unencrypted.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

If a password is not provided in RouterOS versions older than v6.43, then the backup file will be encrypted with the current user's password, except if the dont-encrypted property is used or the current user's password is empty. 

The backup file will be available under `/file` menu, which can be downloaded using FTP or using Winbox.
