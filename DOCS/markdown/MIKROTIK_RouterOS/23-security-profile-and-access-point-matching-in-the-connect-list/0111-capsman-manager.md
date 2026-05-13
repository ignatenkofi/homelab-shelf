## CAPsMAN manager 

**==> picture [516 x 259] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled  (yes | no; Default:  no ) Disable or enable CAPsMAN functionality<br>certificate  (auto | certificate  Device certificate<br>name | none; Default:  none )<br>ca-certificate  (auto | certificate  Device CA certificate<br>name | none; Default:  none )<br>require-peer-certificate  (yes | no;  Require all connecting CAPs to have a valid certificate<br>Default:  no )<br>package-path  (string |; Default: ) Folder location for the RouterOS packages. For example, use "/upgrade" to specify the upgrade folder from the files<br>section. If empty string is set, CAPsMAN can use built-in RouterOS packages, note that in this case only CAPs with<br>the same architecture as CAPsMAN will be upgraded.<br>upgrade-policy  (none | require- Upgrade policy options<br>same-version | suggest-same-<br>upgrade; Default:  none ) none - do not perform upgrade<br>require-same-version - CAPsMAN suggest to upgrade the CAP RouterOS version and if it fails it will not<br>provision the CAP. (Manual provision is still possible)<br>suggest-same-version - CAPsMAN suggests to upgrade the CAP RouterOS version and if it fails it will still be<br>provisioned<br>**----- End of picture text -----**<br>


1468
