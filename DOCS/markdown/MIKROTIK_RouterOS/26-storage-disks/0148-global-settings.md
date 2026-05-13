## Global Settings 

Sub-menu : `/` **`interface ethernet poe settings`** 

Some MikroTik PoE-Out devices support the global PoE settings 

**==> picture [509 x 171] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>ether1- Setting it to "yes" will disable short detection on all poe-out ports. This is potentially dangerous settings and should be used with<br>poe-in- caution.  This feature disables strict input/output current monitoring (short detection) to allow the use of PoE-Out with long ethernet<br>long-cable cables and/or avoiding improper short-circuit detection. It can also affect PoE-Out behavior on PSE which is powered using a DC<br>(yes | no) connector<br>psuX- Specifies the maximum power in watts that the PSU can draw.   default - 96W<br>max-<br>power psu1 - RB5009UPr+S+IN  = DC-jack  | RB5009UPr+S+OUT - 2-PIN<br>psu2 - RB5009UPr+S+IN  = 2-PIN terminal | RB5009UPr+S+OUT - not available<br>This command is designed specifically for RB5009UPr+S+ to ensure the safety and optimal performance of the Power Supply Unit<br>(PSU). It allows users to set the maximum power limit for the PSU, preventing potential overload that could compromise the stability and<br>longevity of the system.<br>**----- End of picture text -----**<br>
