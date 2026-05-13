## Summary 

It is possible to connect the GSM modem to the RouterOS device and use it to send and receive SMS messages. RouterOS lists such modem as a serial port that appears in the ' `/port print` ' listing. GSM standard defines AT commands for sending SMS messages and defines how messages should be encoded in these commands. `'/tool sms send'` uses standard GSM AT commands to send SMS.
