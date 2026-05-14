## CAPs mode script 

A RouterOS CAPs mode script that will override RouterOS default CAPs mode script. It is possible to reapply the factory passwords by utilizing the readonly variables $defconfPassword and $defconfWifiPassword (available starting from RouterOS 7.15). 

**==> picture [13 x 13] intentionally omitted <==**

Any reset button mode will restore the default configuration from the branding package. The CAPs mode script can only be applied via the GUI or CLI by performing a configuration reset after the device has fully booted. 

**==> picture [13 x 13] intentionally omitted <==**

If a Default configuration or CAPs mode script execution takes more than 2 minutes, a script will fail, and LOG will contain "runtime limit exceeded" or in rare cases "std failure: timeout" error. 

211
