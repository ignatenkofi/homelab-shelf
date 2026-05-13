## ThingsBoard preparation 

1567 

Check the guide over here to understand how the ThingsBoard and the RouterOS can be set up to utilize MQTT communication. 

**==> picture [13 x 13] intentionally omitted <==**

This example will showcase access-token scenario for simplicity reasons, but you can use other available options as well. For the production environment, it is suggested to use SSL-MQTT, as non-SSL-MQTT can be easily packet captured and inspected. To understand how to implement SSL-MQTT communication on the instance that is run with the container. Check the guide linked here (Enablin g HTTPS and SSL MQTT section). 

Create 2 KNOTs under the ThingsBoard GUI and make them "gateways". 

Go to the "Devices" section, click on "+" button and "Add new device": 

**==> picture [505 x 121] intentionally omitted <==**

Name the device and checkbox the "Is gateway" option: 

**==> picture [505 x 233] intentionally omitted <==**

Do that for each KNOT that you have: 

**==> picture [505 x 104] intentionally omitted <==**

Set up a unique access token (unique credentials) for each KNOT under the device you've just created, under the "Manage credentials" tab: 

1568 

**==> picture [505 x 177] intentionally omitted <==**
