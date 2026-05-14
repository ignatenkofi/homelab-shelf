## CAPsMAN channel 

Channel group settings allow for the configuration of lists of radio channel related settings, such as radio band, frequency, Tx Power extension channel, and width. 

Channel group settings are configured in the Channels profile menu /caps-man channels 

**==> picture [506 x 208] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>band  (2ghz-b | 2ghz-b/g | 2ghz-b/g/n | 2ghz- Define operational radio frequency band and mode taken from hardware capability of wireless card<br>onlyg | 2ghz-onlyn | 5ghz-a | 5ghz-a/n | 5ghz-<br>onlyn; Default: )<br>comment  (string; Default: ) Short description of the Channel Group profile<br>extension-channel  (Ce | Ceee | eC | eCee |  Extension channel configuration. (E.g. Ce = extension channel is above Control channel, eC =<br>eeCe | eeeC | disabled; Default: ) extension channel is below Control channel)<br>frequency  (integer [0..4294967295]; Default: ) Channel frequency value in MHz on which AP will operate.<br>name  (string; Default: ) A descriptive name for the Channel Group Profile<br>tx-power  (integer [-30..40]; Default: ) TX Power for CAP interface (for the whole interface not for individual chains) in dBm. It is not<br>possible to set higher than allowed by country regulations or interface. By default max allowed by<br>country or interface is used.<br>width  (; Default: ) Sets Channel Width in MHz. (E.g. 20, 40)<br>**----- End of picture text -----**<br>

1463 

save-selected (; Default: yes ) 

Saves selected channel for the CAP Radio - will select this channel after the CAP reconnects to CAPsMAN and use it till the channel Re-optimize is done for this CAP.
