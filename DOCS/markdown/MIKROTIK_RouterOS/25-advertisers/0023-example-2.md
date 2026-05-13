## Example #2 

In the second example, we will showcase another topology: 

**==> picture [505 x 352] intentionally omitted <==**

1576 

We have a few warehouses, a few company delivery vehicles, and 3 assets that we are interested in tracking. Our assets are pallets that hold cargo and our goals are to know: 

- in which specific warehouse (equipped with the KNOT) the asset (equipped with the tag) is currently in and how much time it spent inside the specific warehouse; 

- whether the asset (equipped with the tag) is on the road, traveling between warehouses, and how much time it spent inside the vehicle (equipped with the KNOT); 

- (optionally) if TG-BT5-OUT tags are used , what was the temperature during all this time? You can also/instead monitor other parameters that you can get out of the advertised payload, like for example acceleration; (optionally) find out the KNOT's GPS location. 

To achieve Bluetooth asset-tracking, just install x1 KNOT per warehouse, x1 KNOT per vehicle, and x1 tag per asset. 

We can see that TAG 1 is inside the vehicle, and this vehicle just parked near the warehouse. Both KNOT 1 and KNOT 4 will report to the server that the asset is inside their ranges. This will tell you that the asset is parked but not being transported yet. 

We can see that TAG 2 is traveling between the warehouses and is only inside the KNOT 5 Bluetooth range. In this case, KNOT 5 will be the only reporter and the result that is displayed on the server would mean that the asset is getting transported. 

We can see that TAG 3 is inside the warehouse. The server will indicate just that. 

The data on the server will show the timestamps of each report sent by the KNOT, which will tell you for how long did the asset stay inside the specific device's Bluetooth range.
