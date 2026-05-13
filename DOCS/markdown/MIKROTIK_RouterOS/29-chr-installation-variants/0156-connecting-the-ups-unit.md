## Connecting the UPS unit 

The serial APC UPS (BackUPS Pro or SmartUPS) requires a special serial cable (unless connected with USB). If no cable came with the UPS, a cable may be ordered from APC or one can be made "in-house". Use the following diagram: 

**==> picture [222 x 88] intentionally omitted <==**

**----- Start of picture text -----**<br>
Router Side (DB9f) Signal Direction UPS Side (DB9m)<br>2 Receive IN 2<br>3 Send OUT 1<br>5 Ground 4<br>7 CTS IN 6<br>**----- End of picture text -----**<br>


If using a RouterBOARD device, make sure to set your "RouterBOOT setup key" to Delete instead of the default Any key. This is to avoid accidental opening of the setup menu if the UPS unit sends some data to the serial port during RouterBOARD startup. This can be done in the RouterBOOT options during boot time or via the RouterBoard Settings in Winbox : 

```
Select key which will enter setup on boot:
```

```
* 1 - any key
  2 - <Delete> key only
your choice:
```
