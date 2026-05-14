## Default configuration 

A RouterOS default configuration file that will override RouterOS default configuration. This configuration will persist even after a RouterOS reset. Factory passwords can be reapplied using the read-only variables $defconfPassword and $defconfWifiPassword (access to factory passwords is available starting RouterOS 7.10). 

**==> picture [13 x 13] intentionally omitted <==**

If a Default configuration or CAPs mode script execution takes more than 2 minutes, a script will fail, and LOG will contain "runtime limit exceeded" or in rare cases "std failure: timeout" error.
