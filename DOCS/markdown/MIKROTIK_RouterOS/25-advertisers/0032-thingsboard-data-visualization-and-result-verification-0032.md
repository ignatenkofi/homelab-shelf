## ThingsBoard data visualization and result verification 

After you run the script with `/system script run tracking` or via a scheduler and refresh the GUI portal → all MAC addresses (tags) that are found in the JSON message, will be made into new devices under the ThingsBoard GUI: 

**==> picture [505 x 155] intentionally omitted <==**

To help you visualize the data, you can use the built-in widgets or create your own one. 

Select the tag's MAC address from the list of devices, go to the "Latest telemetry" section, checkbox KNOT IDs that you wish to monitor, and click on the "Show on widget" button: 

1587 

**==> picture [505 x 165] intentionally omitted <==**

Select a widget that you wish to use, for example under the "Charts" bundle, "Timeseries Bar Chart" and click on "Add to dashboard": 

**==> picture [505 x 224] intentionally omitted <==**

Create a new dashboard and name it, however, you like. Click on "Add": 

**==> picture [505 x 180] intentionally omitted <==**

Change the widget's "Timewindow" from "Realtime-last minute" (which is used by default) to "Realtime-last 5 hours" and disable "data aggregation function" (select "none"): 

1588 

**==> picture [505 x 181] intentionally omitted <==**

To help you better visualize the result, edit the widget and then edit each "KNOT_X" parameter/key. Enable the "Show points" checkbox for each key: 

**==> picture [505 x 235] intentionally omitted <==**

Check the ThingsBoard widget guide for more options that you have. 

The end result would look like this: 

1589 

**==> picture [505 x 214] intentionally omitted <==**

Per the dashboard, we can tell that: 

- from ~11:00 to ~11:30, our asset was inside KNOT_1 Bluetooth range (inside warehouse #1); 

- from ~11:30 to ~11:35, our asset was relocated to the vehicle (KNOT_2) that was parked near the warehouse (the tag was inside both KNOT's ranges); 

- from ~11:35 to ~12:00, the tag was inside the truck (KNOT_2) - traveling to another warehouse; 

- from ~12:00 to ~12:05, the asset was parked outside of warehouse #2, and it was inside both KNOT_2 and KNOT_3 ranges at the same time; from ~12:05 to 12:30, our asset was stored inside warehouse #2 (KNOT_3); 

- from ~12.:30 onwards, the tag was on the road again, inside the truck (KNOT_2).
