## One-way SSL communication scenario 

**==> picture [13 x 13] intentionally omitted <==**

Recommended scenario to use! 

**==> picture [13 x 13] intentionally omitted <==**

This type of authentication requires you to use a server certificate for SSL communication. A server certificate must be generated and uploaded to the ThingsBoard instance. 

To generate a server certificate, use this guide as a reference → generate the certificate (for example, using OPENSSL tool), install/upload it into the correct folder, and enable MQTT SSL in the ThingsBoard configuration file. 

The configuration will be the same as shown in the Access token and MQTT Basic scenarios shown above. So choose either one. 

The only difference, in this case, is the communication between the device and the server (you will only have to slightly change MQTT broker configuration in RouterOS settings which will be shown later on). 

When using this scenario, the communication is going to be encrypted (using SSL) .
