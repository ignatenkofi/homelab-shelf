## Steering properties 

**==> picture [13 x 13] intentionally omitted <==**

Unsolicited 802.11v BSS transition management request functionality is supported stating with 7.21beta2. 

Properties in this category govern mechanisms for advertising potential roaming candidates to client devices. 

1356 

**==> picture [516 x 660] intentionally omitted <==**

**----- Start of picture text -----**<br>
2g-probe- If<br>delay  ( no ye|<br>s Default: no) 1.  This property is set to yes on a 2.4GHz AP and<br>2.  said AP is in a steering neighbor group with at least one 5GHz AP then<br>the 2.4GHz AP will forego responding to the first 3 probe requests from each client in a 60 second interval which have a signal-to-noise<br>ratio of > 35 dB.<br>neighbor- When sending neighbor reports and BSS transition management requests, an AP will list all other APs within its neighbor group as<br>group  (string)  potential roaming candidates.<br>By default, a dynamic neighbor group is created for each set of APs with the same SSID and authentication settings.<br>APs operating in the 5GHz band are indicated to be preferable to ones operating in the 2.4GHz band.<br>A dynamic neighbor group will not be created if EAP is used, it needs to be defined manually.<br>rrm  (no | yes;  Enables sending of 802.11k neighbor reports.<br>Default:  yes )<br>The client may request for the "neighbor report" from the AP, when the device wants to "explore/map" its surroundings (the client<br>device can store the report, and it can use it to roam at once or later).<br>transition- Sets an RSSI threshold for sending unsolicited 802.11v BSS transition management requests. If the client device sits "below" the<br>threshold  (inte configured threshold for the duration of  transition-threshold-time , it gets marked as a "transition candidate".<br>ger; Default:<br>-80 )<br>transition- Define a time, in seconds, for how long the client device can sit "below" the configured  transition-threshold  value, to be marked<br>threshold- as "transition candidate".<br>time  (time<br>interval;<br>Default:  10 )<br>transition- Defines an interval in seconds, using which, the AP will send unsolicited 802.11v BSS transition management requests to the client<br>request- device, if it is a "transition candidate".<br>period  (time<br>interval;  E.g., using the default value (30s), a request will be sent to the client every 30 seconds for  transition-request-count  number of<br>Default:  30 ) total requests.<br>transition- Defines how many unsolicited 802.11v BSS transition management requests should be sent out to the client marked as a "transition<br>request-count  candidate". x1 request is sent out immediately after the client gets "transition candidate" status ("-1" count), and the remaining "count"<br>(count,  will be sent every  transition-request-period .<br>unlimited ;<br>Default: ) 3 E.g., using the default value (3), the 1st request gets sent when a client gets "transition candidate" status, the second request gets sent<br>after  transition-request-period  seconds and the third (last one), after another  transition-request-period .<br>Set to  unlimited  if you want to send requests with out a count limit.<br>transition- Defines the time, for how long the client device can be a "transition candidate" before it gets forcefully deauthenticated. It can be a  time<br>time  (time  interval  in seconds (to deauthenticate the client after the time, which starts running/counting as soon as the device becomes a<br>interval,  "transition candidate", expires), it can be  immediate  (to instantly deauthenticate the client after it becomes a "transition candidate") or<br>immediate |  unlimited  (to never force the client and to continue sending transition requests for the  transition-request-count  amount,<br>unlimited;  every  transition-request-period  seconds).<br>Default:  unlimi<br>ted )<br>Note that with  transition-time=immediate ,  transition-request-period  and  transition-request-count<br>become useless, as the client will get deauthenticated instantly after  transition-threshold-time .<br>wnm  (no | yes Enables sending of solicited 802.11v BSS transition management requests.<br>; Default:  yes )<br>A client may request for a "roaming suggestion" packet that contains "neighbor list", to help the device switch APs. The client device<br>may accept the suggestion and roam at once, or it can ignore the suggestion and keep its current connection.<br>**----- End of picture text -----**<br>


1357 

**==> picture [13 x 13] intentionally omitted <==**

Please understand that the client can ignore BSS transition management requests . BBS transition request is a "suggestion" for the client to look for other-better signal APs. After receiving the transition request, it is 100% up to the client to decide whether it wants to switch APs or whether it wants to stay connected to the current AP. 

**==> picture [13 x 13] intentionally omitted <==**

Solicited 802.11v BSS transition management request behaviour: 

A solicited 802.11v BSS transition management packet is sent to the client, per the client's own request. The client device "asks" the AP to provide a "roaming suggestion" (with a "neighbor list") and the AP responds with a transition request (containing the "neighbor list"). 

**==> picture [13 x 13] intentionally omitted <==**

Unsolicited 802.11v BSS transition management request behaviour: 

An unsolicited 802.11v request is sent to the client, without waiting for the client to request it. The request gets sent, even if the client was not asking for it. 

If the client's signal gets below `transition-threshold` (default value: -80 dBm) for longer than `transition-threshold-time` (default value: 10 s), then the client gets marked as a "transition candidate". If the client's signal gets above the `transition-threshold` , then the client's "transition candidate" status gets removed. 

If the client is a "transition candidate", then it will start receiving unsolicited 802.11v BSS transition management request packets (packets "suggesting" to move to other nearby APs). The first such packet will be sent immediately after the client's status changes to the "transition candidate", and the follow-up packets will be sent every `transition-request-period` (default value: 30 s). The `transition-requestcount` (default value: 3) number of transition requests will be sent out in total, after which, the AP will stop suggesting the transition (unless `tra nsition-request-count=unlimited` is configured, which makes the AP send out requests non-stop, one request every `transitionrequest-period` ). After the `transition-request-count` number is run out, the client will get the next transition request either after the client requests it itself, or after the client gets unmarked and marked as a "transition candidate" again. 

The value in `transition-time` defines for how long the client device can stay as a "transition candidate", before it gets forcefully disconnected. Possible `transition-time` values: unlimited (to continue sending transition requests using `transition-request-period` for the amount of `transition-request-count` and to never forcefully deauthenticate the client), configurable time in seconds (to continue sending transition requests using the `transition-request-period` interval and `transition-request-count` number, and then to disconnect the client after the configured `transition-time` has run out), and immediate (to send a transition request to the client, when it becomes a "transition candidate", and to instantly disconnect it).
