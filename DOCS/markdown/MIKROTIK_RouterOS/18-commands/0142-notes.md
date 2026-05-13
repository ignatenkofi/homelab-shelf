## Notes 

Rebooting the router will reset the run-count counter. 

If more than one script has to be executed simultaneously, they are executed in the order they appear in the scheduler configuration. This can be important if one scheduled script is used to disable another one. 

If a more complex execution pattern is needed, it can usually be done by scheduling several scripts, and making them enable and disable each other. 

Note: if scheduler item has start-time set to startup, it behaves as if start-time and start-date were set to time 3 seconds after console starts up. It means that all scripts having `start-time is startup` and `interval is 0` will be executed once each time router boots. If the interval is set to value other than 0 scheduler will not run at startup
