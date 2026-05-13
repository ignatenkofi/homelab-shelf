## Port PFC Stats 

Example `[admin@crs317] /interface/ethernet/switch/qos/port> print pfc interval=1 where running name:  sfp-sfpplus1 sfp-sfpplus2   ether1 pfc:          roce     disabled disabled pfc-tx:            46 pfc-paused-tc:             3 pfc3-pause-threshold:     1 048 576 pfc3-resume-threshold:        10 240 pfc3-use:     1 075 200` 

**==> picture [516 x 216] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name Port name.<br>pfc PFC profile name.<br>pfc-rx Received PFC frame count.<br>pfc-tx Transmitted PFC frame count.<br>pfc-paused-tc The list of traffic classes should be paused (from the sender's perspective). PFC pause frames (XOFF) are periodically<br>sent with the listed timers set from this port.<br>pfc0-pause-threshold ..  Pause thresholds of the respective traffic classes. Only PFC-enabled traffic classes are displayed.<br>pfc7-pause-threshold<br>pfc0-resume-threshold ..  Resume thresholds of the respective traffic classes. Only PFC-enabled traffic classes are displayed.<br>pfc7-resume-threshold<br>pfc0-use .. pfc7-use The current buffer usage of the respective traffic classes (in bytes). In other words, it is the total size of all queued packets<br>on all ports that were received from this port. Only PFC-enabled traffic classes are displayed.<br>**----- End of picture text -----**<br>
