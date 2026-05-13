## ThingsBoard data visualization and result verification 

After you run the script with `/system script run tracking` or via a scheduler and refresh the GUI portal → all MAC addresses (tags) that are found in the JSON message, will be made into new devices under the ThingsBoard GUI: 

1572 

**==> picture [505 x 155] intentionally omitted <==**

To help you visualize the data, you can use the built-in widgets or create your own one. 

Select the tag's MAC address from the list of devices, go to the "Latest telemetry" section, checkbox the "reporter" parameter, and click on the "Show on widget" button: 

**==> picture [505 x 174] intentionally omitted <==**

Select a widget that you wish to use, for example under the "Cards" bundle, "Timeseries table" and click on "Add to dashboard": 

**==> picture [505 x 277] intentionally omitted <==**

1573 

Create a new dashboard and name it, however, you like. Click on "Add": 

**==> picture [505 x 244] intentionally omitted <==**

Do the same steps for your other tags that appeared under the "Devices" tab. Create a new widget for each unique tag under the same dashboard. 

Change the widget's "Timewindow" from "Realtime-last minute" (which is used by default) to "Realtime-current day": 

**==> picture [505 x 244] intentionally omitted <==**

As a result, if both tags are inside the KNOT A range , the dashboard would show: 

1574 

**==> picture [505 x 249] intentionally omitted <==**

If they move to the KNOT B range , it would show: 

**==> picture [505 x 251] intentionally omitted <==**

If the tags move to the overlapped area , inside both ranges, both reporters (KNOT_A and KNOT_B) should show up within a few seconds after each other, depending on the interval used in the scheduler: 

1575 

**==> picture [505 x 250] intentionally omitted <==**
