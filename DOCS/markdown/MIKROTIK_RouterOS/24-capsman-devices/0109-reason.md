## <REASON> 

"joining failed" - can only happen on Prism cards in station mode, failed to connect to AP due to some reason 

"join timeout" - happens on Station, failed to synchronize to AP (receive first beacon frame). Most likely weak signal, remote turned off, strong interference, some other RF related issue that makes communication impossible. 

"no beacons" - no beacons received from remote end of WDS link. Most likely weak signal, remote turned off, strong interference, some other RF related issue that makes communication impossible. 

"extensive data loss" - local interface decided to drop connection to remote device because of inability to send data to remote after multiple failures at lowest possible rate. Possible causes - too weak signal, remote device turned off, strong interference, some other RF related issue that makes communication impossible. 

1539 

"decided to deauth, <802.11 reason>" - local interface decided do deauthenticate remote device using 802.11 reason <802.11 reason>. 

"inactivity" - remote device was inactive for too long 

"device disabled" - local interface got disabled 

"got deauth, <802.11 reason>" - received deauthentication frame from remote device, 802.11 reason code is reported in <802.11 reason> 

"got disassoc, <802.11 reason>" - received disassociation frame from remote device, 802.11 reason code is reported in <802.11 reason> 

"auth frame from AP" - authentication frame from remote device that is known to be AP, most likely mode changes on remote device from AP to Station. 

"bad ssid" - bad ssid for WDS link 

"beacon from non AP" - received beacon frame from remote device that is known to be non-AP node, most likely mode changes on remote device from Station to AP. 

"no WDS support" - does not report WDS support 

"failed to confirm SSID" - failed to confirm SSID of other end of WDS link. 

"hardware failure" - some hardware failure or unexpected behavior. Not likely to be seen. 

"lost connection" - can only happen on Prism cards in station mode, connection to AP lost due to some reason. 

"auth failed <802.11 status>" - happens on Station, AP denies authentication, 802.11 status code is reported in <802.11 status>. 

"assoc failed <802.11 status>" - happens on Station, AP denies association, 802.11 status code is reported in <802.11 status>. 

"auth timeout" - happens on Station, Station does not receive response to authentication frames, either bad link or AP is ignoring this Station for some reason. 

"assoc timeout" - happens on Station, Station does not receive response to association frames, either bad link or AP is ignoring this Station for some reason. 

"reassociating" - happens on AP: connection assumed to be lost, because Station that is considered already associated attempts to associate again. All connection related information must be deleted, because during association process connection parameters are negotiated (therefore "disconnected"). The reason why Station reassociates must be looked for on Station (most likely cause is that Station for some reason dropped connection without telling AP - e. g. data loss, configuration changes). 

"compression setup failure" - connection impossible, because not enough resources to do compression (too many stations that want to use compression already connected) 

"control frame timeout" - AP was unable to transmit to the client (similar to error message that you see in the 802.11 protocol - extensive data loss)
