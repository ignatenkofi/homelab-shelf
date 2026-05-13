## Properties 

**==> picture [498 x 450] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>paypal-allow  (yes | no; Default:  no ) Whether to enable PayPal functionality for User Manager.<br>paypal-currency  (string; Default:  USD ) The currency related to price setting in which users will be billed.<br>paypal-password  (string; Default: ) The password of your PayPal API account.<br>paypal-signature  (string; Default: ) Signature of your PayPal API account.<br>paypal-use-sandbox  (yes | no; Default:  no ) Whether to use PayPal's sandbox environment for testing purposes.<br>paypal-user  (string; Default: ) Username of your PayPal API account.<br>web-private-password  (string; Default: ) Password for accessing /um/PRIVATE/ section over HTTP.<br>web-private-username  (string; Default: ) Username for accessing /um/PRIVATE/ section over HTTP.<br>Users<br>Sub-menu: /user-manager user<br>Properties<br>Property Description<br>attributes  (array of attributes; Default: ) Custom set of  Attributes  with their values that will additionally be added to Access-Accept messages.<br>caller-id  (string; Default: ) Allow user's authentication with a specific Calling-Station-Id value.<br>comment  (string; Default: ) Short description of the user.<br>disabled  (yes | no; Default:  no ) Controls whether the user can be used or not.<br>group  (group; Default:  default ) Name of the  Group  the user is associated to.<br>name  (string; Default: ) Username for session authentication.<br>otp-secret  (string; Default: ) A one-time password token that is attached to the password.<br>password  (string; Default: ) The password of the user for session authentication.<br>shared-users  (integer | unlimited; Default: ) 1 The total amount of sessions the user can simultaneously establish.<br>**----- End of picture text -----**<br>


Commands 

Property Description add-batch-users () The command can generate multiple user accounts based on various parameters. generate-voucher Generates a file based on voucher-template that can be presented to the end user. () 

338 

monitor () 

Shows total statistics for a user. Stats include total-uptime, total-download, total-upload, active-sessions, actual-profile, attributesdetails.
