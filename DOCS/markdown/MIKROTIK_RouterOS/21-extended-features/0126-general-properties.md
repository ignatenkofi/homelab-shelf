## General Properties 

**==> picture [516 x 131] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>alarm-setting  (delayed | immediate | low- UPS sound alarm setting:<br>battery | none; Default:  immediate )<br>delayed - alarm is delayed to the on-battery event<br>immediate - alarm immediately after the on-battery event<br>low-battery - alarm only when the battery is low<br>none - do not alarm<br>check-capabilities  (yes | no; Default:  yes ) Whether to check UPS capabilities before reading information. Disabling it can fix compatibility issues with<br>some UPS models. (Applies to RouterOS version 6, implemented since v6.17)<br>**----- End of picture text -----**<br>

1901 

**==> picture [516 x 165] intentionally omitted <==**

**----- Start of picture text -----**<br>
min-runtime  (time; Default:  never ) Minimal run time remaining. After a 'utility' failure, the router will monitor the runtime-left value. When the<br>value reaches the min-runtime value, the router will go to hibernate mode.<br>never - the router will go to hibernate mode when the "battery low" signal is sent indicating that the<br>battery power is below 10%<br>0s - the router will continue to work as long as the battery is supplying sufficient voltage<br>offline-time  (time; Default:  0s ) How long to work on batteries. The router waits that amount of time and then goes into hibernate mode<br>until the UPS reports that the 'utility' power is back<br>0s - the router will go into hibernate mode according to the min-runtime setting. In this case, the router<br>will wait until the UPS reports that the battery power is below 10%<br>port  (string; Default: ) Communication port of the router.<br>**----- End of picture text -----**<br>

Read-only properties: 

**==> picture [516 x 267] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>load  (percent) The UPS's output load as a percentage of full rated load in Watts. The typical accuracy of this measurement is ±3% of the<br>maximum of 105%<br>manufacture-date  (string) UPS's date of manufacture in the format "mm/dd/yy" (month, day, year).<br>model  (string) Less than 32 ASCII character string consisting of the UPS model name (the words on the front of the UPS itself)<br>nominal-battery-voltage  ( UPS's nominal battery voltage rating (this is not the UPS's actual battery voltage)<br>integer)<br>offline-after  (time) When will the router go offline<br>serial  (string) A string of at least 8 characters directly representing the UPS's serial number as set at the factory. Newer SmartUPS models<br>have 12-character serial numbers<br>version  (string) UPS version, consists of three fields: SKU number, firmware revision, country code. The country code may be one of the<br>following:<br>I - 220/230/240 Vac<br>D - 115/120 Vac<br>A - 100 Vac<br>M - 208 Vac<br>J - 200 Vac<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

Note: In order to enable UPS monitor, the serial port should be available.
