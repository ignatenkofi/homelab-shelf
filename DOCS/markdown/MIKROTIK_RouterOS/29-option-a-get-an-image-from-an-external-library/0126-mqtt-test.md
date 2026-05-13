## MQTT test 

Log in with the tenant and create a new device. Go to the " Devices " menu, click on the " + " (Add Device) button and choose the " Add new device " option: 

**==> picture [505 x 121] intentionally omitted <==**

Name it, however, you like, and click on " Add ": 

1888 

**==> picture [505 x 235] intentionally omitted <==**

Check your device access token by clicking on the device you've just created and selecting the " Manage credentials " setting (copy the access token generated or type in your own →  "YOUR_TOKEN"): 

**==> picture [505 x 175] intentionally omitted <==**

After these steps, go to the RouterOS settings (back to CHR settings) and create a new MQTT broker ( make sure that you have IoT package installed beca use otherwise, you will not have this menu): 

```
/iot/mqtt/brokers/add name=tb address=172.18.0.2 port=1883 username=YOUR_TOKEN
```
