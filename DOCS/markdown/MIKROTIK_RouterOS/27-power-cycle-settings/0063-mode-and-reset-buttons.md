## Mode and Reset buttons 

Reset button additional functionality is supported by all MikroTik devices running RouterOS 

Some RouterBOARD devices have a mode button that allows you to run any script when the button it pushed. 

The list of supported devices: 

RBcAP-2nD (cAP) RBcAPGi-5acD2nD (cAP ac) RBwsAP5Hac2nD (wsAP ac lite) RB750Gr3 (hEX) RB760iGS (hEX S) RB912R-2nD (LtAP mini, LtAP mini LTE/4G kit) RBD52G-5HacD2HnD (hAP ac^2) RBLHGR (LHG LTE/4G kit) RBSXTR (SXT LTE/4G kit) CRS328-4C-20S-4S+RM CRS328-24P-4S+RM CCR1016-12G r2 CCR1016-12S-1S+ r2 CCR1036-12G-4S r2 

1749 

CCR1036-8G-2S+ r2 

- RBD53G-5HacD2HnD (Chateau) RBD53GR-5HacD2HnD (hAP ac^3) E50UG (hEX) 

- L41G-2axD (hAP ax lite) 

- L009UiGS-RM, L009UiGS-2HaxD-IN cAPGi-5HaxD2HaxD (cAP ax) C53UiG+5HPaxD2HPaxD (hAP ax^3) S53UG+5HaxD2HaxD (Chateau ax) H53UiG-5HaxQ2HaxQ (Chateau PRO ax) CCR2116-12G-4S+ 

RDS2216-2XG-4S+4XS-2XQ 

**==> picture [506 x 111] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled  (no | yes; Default: no ) Disable or enable the operation of the button<br>hold-time  (time interval Min..Max;  HoldTime:= Button functionality can be called if a button is pressed for a certain period of time:<br>Default: ) Min..Max: Min -- 0s..1m (time interval), Max -- 0s..1m (time interval) (available only starting from RouterOS<br>6.47beta60)<br>on-event  (string; Default: ) Name of the script that will be run upon pressing the button. The script must be defined and named in the "<br>/system scripts" menu<br>**----- End of picture text -----**<br>
