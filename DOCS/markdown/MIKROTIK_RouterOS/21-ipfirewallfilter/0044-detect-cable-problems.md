## Detect Cable Problems 

A cable test can detect problems or measure the approximate cable length if the cable is unplugged on the other end and there is, therefore, "no-link". RouterOS will show: 

which cable pair is damaged the distance to the problem how exactly the cable is broken - short-circuited or open-circuited 

This also works if the other end is simply unplugged - in that case, the total cable length will be shown. 

Here is an example output: 

```
[admin@CCR] > interface ethernet cable-test ether2
name: ether2
status: no-link
cable-pairs: open:4,open:4,open:4,open:4
```

1306 

In the above example, the cable is not shorted but “open” at 4 meters distance, all cable pairs are equally faulty at the same distance from the switch chip. 

Currently `cable-test` is implemented on the following devices: 

**==> picture [182 x 287] intentionally omitted <==**

**----- Start of picture text -----**<br>
Devices<br>CCR1xxx series devices RB952Ui-5ac2nD<br>CRS1xx series devices RB962UiGS-5HacT2HnT<br>CRS2xx series devices RB1100AHx2<br>OmniTIK series devices RB1100x4<br>RB450G series devices RBD52G-5HacD2HnD<br>RB951 series devices RBcAPGi-5acD2nD<br>RB2011 series devices RBmAP2n<br>RB4011 series devices RBmAP2nD<br>RB750Gr2 RBwsAP-5Hac2nD<br>RB750UPr2 RB3011UiAS-RM<br>RB751U-2HnD RBMetal 2SHPn<br>RB850Gx2 RBDynaDishG-5HacD<br>RB931-2nD RBLDFG-5acD<br>RB941-2nD RBLHGG-5acD<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Currently `cable-test` is not supported on Combo ports.
