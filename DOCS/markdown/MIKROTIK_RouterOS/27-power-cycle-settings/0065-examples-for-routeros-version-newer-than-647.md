## Examples for RouterOS version newer than 6.47: 

```
/system script add name=test-mode-button source={:log info message=("mode button pressed");}
/system routerboard mode-button set on-event=test-mode-button hold-time=3..5 enabled=yes
```

The reset button works in the same way, but the menu is moved under the : `/system routerboard reset-button` : 

```
/system script add name=test-reset-button source={:log info message=("reset button pressed");}
/system routerboard reset-button set on-event=test-reset-button hold-time=0..10 enabled=yes
```

LED dark mode control with the mode button: 

```
/system script add name=dark-mode source={
   :if ([system leds settings get all-leds-off] = "never") do={
      /system leds settings set all-leds-off=immediate
   } else={
        /system leds settings set all-leds-off=never
   }
 }
/system routerboard mode-button set enabled=yes on-event=dark-mode
```

The D53, C53, S53 and H53 series RouterBoards have configurable WPS button. It also works in the same way as reset button and mode button and executes a script. 

1750 

```
/system script add name=test-wps-button source={:log info message=("wps button pressed");}
```

```
/system routerboard wps-button set on-event=test-wps-button hold-time=0..10 enabled=yes
```

WPS accept control with the WPS button or the Mode button: 

```
/system script add name=wps-accept source={
    :foreach iface in=[/interface/wifi find where (configuration.mode="ap" && disabled=no)] do={
        /interface/wifi wps-push-button $iface;}
}
```

```
/system routerboard wps-button set enabled=yes on-event=wps-accept
```

```
/system routerboard mode-button set enabled=yes on-event=wps-accept
```

1751
