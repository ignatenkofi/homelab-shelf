## GPS coordinate visualization (optional) 

Per the script in the Script that includes GPS data section, the script sends x2 MQTT messages. Each message is sent to a different MQTT topic. GPS coordinate message will be posted to a topic named "1/devices/me/telemetry", while Bluetooth data will be posted to a topic named "v1/gateway /telemetry". Coordinates will be available to you under the ThingsBoard device list, under the specific gateway: 

**==> picture [505 x 160] intentionally omitted <==**

Checkbox both "latitude" and "longitude" parameters, click on the "Show on widget button", select "Current bundle" to "Maps", and choose the "Route Map - OpenStreetMap" widget: 

1591 

**==> picture [505 x 253] intentionally omitted <==**

To finish things up, click on the "Add to dashboard" button and choose the dashboard where you want the widget to be shown. 

After adding 3 widgets into 1 dashboard (temperature line chart, Bluetooth reporter bar chart, and GPS coordinates map), you would get something similar to this: 

**==> picture [505 x 252] intentionally omitted <==**

You will have a graph showing temperature changes (the tag's surrounding temperature); You will have the chart that indicates which specific KNOT has sent the report, that tells you in which KNOT's Bluetooth range the tag is currently in; 

You will have a map that shows the GPS position of the KNOT. 

1592
