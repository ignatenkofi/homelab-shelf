## <DEV>: data from unknown device <MAC>, sent deauth [(XXX events suppressed, YYY deauths suppressed)] 

Data frame from unknown device (read - not registered to this AP) with mac address <MAC> received, AP sent deauthentication frame to it (as per 802.11). XXX is number of events that are not logged so that the log does not become too large (logs are limited to 1 entry per 5s after first 5 entries), YYY is the number of deauthentication frames that should have been sent, but were not sent, so that resources are not wasted sending too many deauthentication frames (only 10 deauth frames per second are allowed). 

The likely cause of such a message is that the Station previously connected to the AP, which does not yet know it has been dropped from AP registration table, sending data to AP. Deauthentication message tells the Station that it is no longer connected.
