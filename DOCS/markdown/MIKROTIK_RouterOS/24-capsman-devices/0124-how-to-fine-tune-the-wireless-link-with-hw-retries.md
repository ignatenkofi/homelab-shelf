## How to fine-tune the wireless link with hw-retries? 

You should understand that for 802.11 devices there is a really limited amount of information (or "feedback" from the environment) that devices can use to tune their behavior: 

signal strength, which could be used to figure out best transmit rate knowing receiver sensitivity. Sill this is not reliable taking into account that sensitivity for different receivers varies (e.g. changes over time), path conditions are not symmetric (and device can only measure signal strength it receives), etc. 

by receiving/not receiving acknowledgment for frame sent. 

Taking into account that using signal strength is not reliable, 802.11 devices are essentially left with only one "feedback" to tune its operation - success /failure of transmission. When transmission fails (ACK not received in time), there is no way how sender can figure out why it failed - either because of noise, multipath, direct interference (and whether that disturbed actual data frame or the ACK itself) - frame just did not make it and in general it does not matter "why". All that matters is the packet error rate. 

Therefore RouterOS implements an algorithm to try to use medium most efficiently in any environment by using only this limited information, giving users the ability to control how the algorithm works and describing the algorithm. And there are only a few usage guidelines, not a set of values you should use in a particular situation. 

1542 

In general - the larger hw-retries, the better "feedback" device gets about medium ability to deliver frame at particular rate (e.g. if sending frame with rate 54mbps fails 16 times, it is telling you more than if it fails with 2 retries) and the better it can figure out optimal transmit rate, at the expense of latency it can introduce in network - because during all those failing retries, other devices in this channel cannot send. So bigger hw-retries can be suggested for ptp backbone links - where it is known that link must be always on. Less hw-retries make rate selection adapt faster at the expense of some accuracy (going below 2 is not reasonable in most cases), this can be suggested for ptmp links, where it is normal for links to connect/disconnect and keeping latency down is important. 

on-fail-retry-time and disconnect-timeout controls how hard device will try to consider remote party "connected". Larger disconnect-timeout will make the device not "disconnect" other party, even if there are lots of loss at the smallest possible transmission rate. This again is most useful for "weak" links that are known that they "must" be established (e.g. backbone links). In ptmp networks large disconnect-timeout will again increase latency in the network during the time e.g. AP will attempt to send data to some client that has just been disabled (AP will try to do this for the whole disconnect-timeout). 

frame-lifetime allows to tune for how long AP is attempting to use frame for transmitting before considering that it is not worth delivering it (for example, if sending frame fails at lowest possible rate, on-fail-retry-time timer is enabled, if during this timer frame-lifetime expires, particular frame is dropped and the next transmission attempt will happen with the next frame. Disabled frame-lifetime means that wireless will ensure in order delivery of "all" data frames, no matter how long it takes, "or" will drop the connection if everything fails). This allows optimizing for different types of traffic e.g. for real-time traffic - if the primary use of the wireless network is e.g. voip, then it can be reasonable to limit frame-lifetime, because voip tolerates small loss better than high latency.
