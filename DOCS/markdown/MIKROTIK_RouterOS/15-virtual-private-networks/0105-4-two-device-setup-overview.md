## 4. Two-Device Setup Overview 

This manual focuses on a minimal setup with two devices: 

**==> picture [247 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
Role Device Function<br>Server RouterOS Hosts IPsec tunnel; provides QKD/PPK key<br>Client ROS/LibreSwan Connects to server using QKD/PPK<br>**----- End of picture text -----**<br>

The RouterOS server may act as a QKD client to a KME, so no third device is required.
