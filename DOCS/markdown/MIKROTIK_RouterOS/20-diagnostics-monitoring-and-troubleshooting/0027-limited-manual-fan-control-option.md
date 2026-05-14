## Limited manual fan-control option 

**==> picture [13 x 13] intentionally omitted <==**

Starting from RouterOS version 7.9 limited manual fan-control options have been added for CRS3xx, CRS5xx and CCR2xxx devices. 

Starting from RouterOS version 7.14 limited manual fan-control is available for the CCR1036-8G-2S+-r2, CCR1036-12G-4S-r2 and CCR101612S-1S+-r2 devices. 

Fan behavior can be manipulated using the settings section of system health: 

```
/system health settings set
```

Available properties are described below: 

**==> picture [516 x 101] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>fan-full-speed-temp  (integer [-273..65]; Def Sets the temperature value upon which the fan speed will be increased to the maximum possible rpm.<br>ault:  65 )<br>Reads temperature from CPU, PHY, SWITCH and SFP and adjusts fan speed based on the component<br>with the highest temperature.<br>fan-target-temp  (integer [-273..65]; Default:  Sets the target temperature for the hottest component. Based on this setting adjusts fan behavior to hold<br>58 ) temperatures in target range.<br>**----- End of picture text -----**<br>

1766 

fan-min-speed-percent (integer [0..100]; De Sets the minimum percentage of fan speed thus not allowing fans to have a lower rpm than this value. fault: depends on FAN controller ) *NOTE: the default value may vary based on FAN controller chip and/or specific model requirements. From RouterOS verson 7.14 default value is set to 12, all previous versions have 0. fan-control-interval (integer [5..30]; Default: Sets the actual temperature data read interval to get temperature values from CPU, PHY, SWITCH and 30 ) SFP. *NOTE: THIS SETTING DIRECTLY AFFECTS CPU USAGE cpu-overtemp-check (yes | no; Default: no) Enables/disables CPU overtemperature monitoring. (Available for ARM/ARM64 devices) cpu-overtemp-threshold (integer [0..105]; Maximum temperature before triggering an overtemperature protection. Default: 105) cpu-overtemp-startup-delay (time; Default: Delay after startup before enabling overtemperature monitoring. 1m)
