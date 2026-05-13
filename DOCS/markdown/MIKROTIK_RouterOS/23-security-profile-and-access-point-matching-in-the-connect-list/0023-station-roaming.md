## Station Roaming 

Station Roaming feature is available only for 802.11 wireless protocol and only for station modes. When RouterOS wireless client is connected to the AP using 802.11 wireless protocol it will periodically perform the background scan with specific time intervals. When the background scan will find an AP with better signal it will try to roam to that AP. The time intervals between the background scans will become shorter when the wireless signal becomes worse and the background scan interval will become longer when the wireless client signal will get better.
