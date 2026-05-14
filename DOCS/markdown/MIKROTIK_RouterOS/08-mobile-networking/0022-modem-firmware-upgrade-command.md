## Modem firmware-upgrade command 

Command allows to check and upgrade modem firmware if update is available for supported MikroTik modems. 

For firmware update availability check and installation active internet connection is required, depending on modem internet connection can be provided using any  RouterOS  interface or modem interface (FOTA), please see table bellow regarding each modem supported connection methods. 

**==> picture [516 x 177] intentionally omitted <==**

**----- Start of picture text -----**<br>
Arguments / Properties Description<br>upgrade  (yes | no;  Set command execution mode:<br>Default:  no )<br>no - display current modem firmware version and show latest available firmware version<br>yes - performs firmware installation<br>update-channel  (stable |  Sets which firmware update channel is used:<br>testing; Default:  stable )<br>stable - firmware version for general use<br>testing - early access/testing channel where modem firmware is published before releasing it in stable channel<br>Feature available from v7.17beta2.<br>firmware-file  (string;  Allows to override firmware update source and perform upgrade from custom location (file, url) in environments where<br>Default:"" ) upgrade using internet connection to MikroTik upgrade servers is not a viable option, eg private networks etc.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

Before attempting an LTE modem firmware upgrade - upgrade RouterOS version to the latest release How To Upgrade RouterOS 

Modems with firmware update support and connectivity required 

814 

Use command /interface lte monitor [find] once returned property "model" for installed modem model identification. 

**==> picture [257 x 268] intentionally omitted <==**

**----- Start of picture text -----**<br>
Modem Required connectivity to MikroTik upgrade servers<br>EC200A-EU Using modem LTE interface<br>Using any RouterOS interface(7.18beta1+)<br>R11eL-EC200A-EU<br>EG06-A Using any RouterOS interface<br>EP06-A Using any RouterOS interface<br>EG12-EA Using any RouterOS interface<br>EG18-EA Using any RouterOS interface<br>FG621-EA Using any RouterOS interface<br>R11eL-FG621-EA<br>R11-LTE Using modem LTE interface<br>R11e-4G Using any RouterOS interface<br>R11e-LTE6 Using any RouterOS interface<br>RG502Q-EA Using any RouterOS interface<br>RG520F-EU Using any RouterOS interface<br>**----- End of picture text -----**<br>
