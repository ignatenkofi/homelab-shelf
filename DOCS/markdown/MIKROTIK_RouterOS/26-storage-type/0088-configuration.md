## Configuration 

```
Sub-menu: /lcd
```

**==> picture [516 x 187] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>backlight-timeout  (time interval: 5m..2h | never; Default:  30m ) Time after which LCD touchscreen is turned off<br>color-scheme  (dark | light; Default: depends on RouterBoard model) Changes to color scheme with a dark or light background.<br>default-screen  (informative-slideshow|interfaces|log|main- Default screen that is showed after startup.<br>menu|stat-slideshow|stats|stats-all; Default:  main-menu )<br>enabled  (yes | no; Default:  yes ) Turns LCD touchscreen on/off. When off, it stops and resets statistics gathering<br>and closes the LCD program.<br>read-only-mode  (yes | no; Default:  yes ) Enables or disables Read-Only mode. If Read-Only mode is enabled, then menus<br>which can be used to change configuration are hidden.<br>time-interval  (min | hour | daily | weekly; Default:  min ) Time interval of displayed interface statistics in Stats screen<br>touch-screen  (enabled | disabled, Default:  enabled ) Enable/disable touch screen input.<br>**----- End of picture text -----**<br>


Available functions: 

backlight - Turns on/off LCD touchscreen backlight, LCD program remains working; recalibrate - Starts LCD Touchscreen Calibration process; show - Set the screen which is displayed on the LCD; take-screenshot - Creates image of currently displayed LCD screen.
