## Troubleshooting 

To check the status of RADIUS messages, you can use the radius menu. 

**==> picture [505 x 179] intentionally omitted <==**

Or alternatively via the command line run "/radius monitor X", X being the numerical ID, you can see the IDs with "/radius print". For more information, additional logging can be configured under "/system logging add topics=radius,debug,packet". You can view results under "/log". 

To view active wireless connections check the WiFi registration table (/interface wifi registration-table print). 

1387
