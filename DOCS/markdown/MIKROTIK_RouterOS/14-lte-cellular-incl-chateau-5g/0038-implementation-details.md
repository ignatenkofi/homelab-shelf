## Implementation details 

AT+CMGS and AT+CMGF commands are used. Port is acquired for the duration of the command and cannot be used concurrently by another RouterOS component. Message sending process can take a long time, it times out after a minute and after two seconds during the initial AT command exchange. 

830
