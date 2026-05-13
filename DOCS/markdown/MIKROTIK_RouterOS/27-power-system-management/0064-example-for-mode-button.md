## Example for mode button: 

```
/system script add name=test-mode-button source={:log info message=("mode button pressed");}
/system routerboard mode-button set on-event=test-mode-button enabled=yes
```

Upon pressing the button, the message"mode button pressed" will be logged in the system log. 

**==> picture [13 x 13] intentionally omitted <==**

Starting from RouterOS 6.47 reset-button functionality and a hold-time option have been added
