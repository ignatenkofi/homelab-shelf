## Example #1 

One of the use cases is shown in the topology below: 

**==> picture [505 x 327] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

The scale of objects and Bluetooth operating ranges are just shown as an example, to help visually understand and imagine the topology! 

We have a warehouse area and we have 3 assets (pallets) that we are interested in tracking. We also have 3 zones : zone , where newly arrived pallets A are stored; zone , where our assets are relocated to be inspected; and zone , where assets are moved after inspection. To achieve Bluetooth assetB C tracking, just install x1 KNOT per zone and x1 tag per asset. 

If TAG 1 and TAG 2 (pallets) arrive in the "arrival" zone A, KNOT A will report to the server that both assets are within its Bluetooth range. If TAG 3 gets moved to zone C, the server will indicate it is within the KNOT C range. If TAG 1 and TAG 2 move toward the B zone, and stay on the edges between A and B zones, the server will show that it is in the overlapped area (at the same time within KNOT-A and KNOT-B ranges). If the tags move to the middle of the warehouse, the server will indicate that they are in all 3 zones at once, in the overlapping area.
