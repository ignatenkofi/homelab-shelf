## Parameters: 

**==> picture [13 x 13] intentionally omitted <==**

Starting with the 7.1rc3 firmware release, a new parameter was added, called "data-age" (measured in seconds). This parameter displays the time that has passed since the device received the last NMEA message. 

**==> picture [383 x 136] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>date-and-time  (date) Date and time received from GPS<br>latitude  (none | string) Latitude in DM (Degrees Minute decimal) format<br>longitude  (none | string) Longitude in DM (Degrees Minute decimal) format<br>altitude  (none | string) Altitude based on GPS data<br>speed  (none | string) The current moving speed of the GPS unit<br>destination-bearing  (none | string) The direction toward which a GPS is moving<br>**----- End of picture text -----**<br>


797 

**==> picture [383 x 133] intentionally omitted <==**

**----- Start of picture text -----**<br>
true-bearing  (none | string) The direction toward which a GPS is moving<br>magnetic-bearing  (none | string) The direction toward which a GPS is moving<br>valid  (yes | no)<br>satellites  (integer) Number of satellites seen by the device.<br>fix-quality  (integer) Quality of the signal<br>horizontal-dilution  (integer) Horizontal dilution of precision (HDOP);<br>data-age  (integer) The time that has passed since the device received the last NMEA message<br>**----- End of picture text -----**<br>
