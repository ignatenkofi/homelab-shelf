## Overview 

Package: `wifi-qcom` 

It is no secret, that Wi-Fi range for indoor access points is limited. It is affected, mostly, by local regulations, which restrict device's output power (depending on which frequency channel is used). A typical indoor Wi-Fi connection is established between an AP (access point) and a client (station) device (smartphone, laptop...etc.). 

Indoor APs are, usually, equipped with omnidirectional antennas (which allow broadcasting the signal in a "donut" shape around the AP), which have a relatively low antenna gain. For indoor and short distance outdoor installations, it is a perfect antenna to use. Using a simple home AP with omnidirection antennas, you can achieve a distance of up to ±100 meters in the "ideal" interference-free line of sight setup. Which is reduced much further inside buildings. 

However! If you were to increase the antenna gain of the AP and "direct" the signal in a smaller angle towards a specific destination (instead of broadcasting the signal in 360°), you could achieve a much longer distance connection (if the station device is positioned within the directed angle). This is where outdoor long-range APs and CPEs come into play. They allow establishing Wi-Fi connections over multiple kilometer distances. 

Long distance connections require you to have a device running in "AP" mode and a client-side device, running in "station" mode. Multiple stations can be connected to a single AP. 

**==> picture [13 x 12] intentionally omitted <==**

This guide is meant for 802.11 AX devices running **`wifi-qcom`** package/drivers.
