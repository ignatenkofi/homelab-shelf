## Registration Table 

Sub-menu: `/interface wireless registration-table` 

In the registration table, you can see various information about currently connected clients. It is used only for Access Points. 

All properties are read-only. 

**==> picture [504 x 202] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>802.1x- whether the data exchange is allowed with the peer (i.e., whether 802.1x authentication is completed, if needed)<br>port-<br>enabled  (y<br>es | no)<br>ack- current value of ack-timeout<br>timeout  (in<br>teger)<br>ap  (yes |  Shows whether registered device is configured as access point.<br>no)<br>ap-tx-limit  ( transmit rate limit on the AP, in bits per second<br>integer)<br>authentica authentication method used for the peer<br>tion-type  ()<br>**----- End of picture text -----**<br>

1410 

**==> picture [504 x 687] intentionally omitted <==**

**----- Start of picture text -----**<br>
bridge  (ye<br>s | no)<br>bytes  (inte number of sent and received packet bytes<br>ger ,<br>integer)<br>client-tx- transmit rate limit on the AP, in bits per second<br>limit  (integ<br>er)<br>comment  ( Description of an entry. comment is taken from appropriate Access List entry if specified.<br>string)<br>compressi whether data compresson is used for this peer<br>on  (yes |<br>no)<br>distance  (i<br>nteger)<br>eap- EAP identity the client used when authenticating to RADIUS server.<br>identity  (st<br>ring)<br>encryption unicast encryption algorithm used<br>(aes-ccm<br>| tkip)<br>evm-ch0  ()<br>evm-ch1  ()<br>evm-ch2  ()<br>frame- number of sent and received data bytes excluding header information<br>bytes  (inte<br>ger,<br>integer)<br>frames  (int Number of frames that need to be sent over wireless link. This value can be compared to hw-frames to check wireless retransmits. Rea<br>eger, d more >><br>integer)<br>framing- current size of combined frames<br>current-<br>size  (integ<br>er)<br>framing- maximal size of combined frames<br>limit  (integ<br>er)<br>framing- the method how to combine frames<br>mode  ()<br>group- group encryption algorithm used<br>encryption<br>()<br>hw-frame- number of sent and received data bytes including header information<br>bytes  (inte<br>ger,<br>integer)<br>hw-frames Number of frames sent over wireless link by the driver. This value can be compared to frames to check wireless retransmits. Read<br>(integer, more >><br>integer)<br>**----- End of picture text -----**<br>

1411 

**==> picture [504 x 689] intentionally omitted <==**

**----- Start of picture text -----**<br>
interface  ( Name of the wireless interface to which wireless client is associated<br>string)<br>last- last interface data tx/rx activity<br>activity  (ti<br>me)<br>last-ip  (IP  IP address found in the last IP packet received from the registered client<br>Address)<br>mac- MAC address of the registered client<br>address  (<br>MAC)<br>managem<br>ent-<br>protection  (<br>yes | no)<br>nstreme  (y Shows whether Nstreme is enabled<br>es | no)<br>p- estimated approximate throughput that is expected to the given peer, taking into account the effective transmit rate and hardware<br>throughput retries. Calculated once in 5 seconds<br>(integer)<br>packed- number of bytes packed into larger frames for transmitting/receiving (framing)<br>bytes  (inte<br>ger,<br>integer)<br>packed- number of frames packed into larger ones for transmitting/receiving (framing)<br>frames  (int<br>eger,<br>integer)<br>packets  (i number of sent and received network layer packets<br>nteger.<br>integer)<br>radio- radio name of the peer<br>name  (stri<br>ng)<br>routeros- RouterOS version of the registered client<br>version  (st<br>ring)<br>rx-ccq  () Client Connection Quality (CCQ) for receive.  Read more >><br>rx-rate  (int receive data rate<br>eger)<br>signal- average strength of the client signal recevied by the AP<br>strength  (i<br>nteger)<br>signal-<br>strength-<br>ch0  ()<br>signal-<br>strength-<br>ch1  ()<br>signal-<br>strength-<br>ch2  ()<br>**----- End of picture text -----**<br>

1412 

**==> picture [504 x 674] intentionally omitted <==**

**----- Start of picture text -----**<br>
signal-to-<br>noise  ()<br>strength- signal strength level at different rates together with time how long were these rates used<br>at-rates  ()<br>tdma-retx<br>()<br>tdma-rx-<br>size  ()<br>tdma- tdma-timing-offset is proportional to distance and is approximately two times the propagation delay. AP measures this so that it can tell<br>timing- clients what offset to use for their transmissions - clients then subtract this offset from their target transmission time such that<br>offset  () propagation delay is accounted for and transmission arrives at AP when expected. You may occasionally see small negative value (like<br>few usecs) there for close range clients because of additional unaccounted delay that may be produced in transmitter or receiver<br>hardware that varies from chipset to chipset.<br>tdma-tx- Value in bytes that specifies the size of data unit whose loss can be detected (data unit over which CRC is calculated) sent by device.<br>size  (integ In general - the bigger the better, because overhead is less. On the other hand, small value in this setting can not always be<br>er) considered a signal that connection is poor - if device does not have enough pending data that would enable it to use bigger data units<br>(e.g. if you are just pinging over link), this value will not go up.<br>tdma-<br>windfull  ()<br>tx-ccq  () Client Connection Quality (CCQ) for transmit.  Read more >><br>tx-evm-<br>ch0  ()<br>tx-evm-<br>ch1  ()<br>tx-evm-<br>ch2  ()<br>tx-frames-<br>timed-out<br>()<br>tx-rate  ()<br>tx-signal-<br>strength  ()<br>tx-signal-<br>strength-<br>ch0  ()<br>tx-signal-<br>strength-<br>ch1  ()<br>tx-signal-<br>strength-<br>ch2  ()<br>uptime  (ti time the client is associated with the access point<br>me)<br>wds  (yes |  whether the connected client is using wds or not<br>no)<br>wmm- Shows whether WMM is enabled.<br>enabled  (y<br>es | no)<br>**----- End of picture text -----**<br>

1413
