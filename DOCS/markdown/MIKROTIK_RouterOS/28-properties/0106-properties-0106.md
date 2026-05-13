## Properties 

**==> picture [516 x 152] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>latency-distribution- Maximal latency range for latency distribution measurements. Based on this value, RouterOS will decide what latency range to<br>max  (time; Default:  10 use as the latency-distribution-measure-interval property<br>0us )<br>measure-out-of-order  ( Whether to measure Out-of-Order packets. The default value is based on CPU type (multi-core CPU default  no ; single-core<br>yes | no; Default: ) CPU default  yes ). When the property is enabled on the multi-core device, a single stream will utilize only a single CPU core<br>stats-samples-to-keep How many data examples to collect<br>(integer; Default:  100 )<br>test-id  (integer [0..255]<br>; Default: ) 0<br>**----- End of picture text -----**<br>


Read-Only Properties 

1831 

**==> picture [516 x 406] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>latency-distribution-samples  (integer) Shows how many individual time periods the latency-distribution-measure-interval is divided into<br>latency-distribution-measure-interval  (time) Shows total latency measurement range<br>running  (yes | no) Shows whether the traffic generator tool is started.<br>Commands<br>Property Description<br>quick  () This command allows to quickly start the packet generator and print the stats output to the terminal. Command also accepts several<br>parameters that override settings in packet template and stream settings. Accepted parameters are  duration, entries-to-show, freeze-frame-<br>interval, id, interface, mbps, measure-out-of-order, packet-count, packet-size, port, pps, stream, test-id, tx-template<br>tx-template - packet templates to generate traffic (max 16 templates)<br>duration - how long to run the test<br>entries-to-show - how many status lines print to the terminal<br>freeze-frame-interval - how often to update the status to the terminal<br>The rest of the parameters are not command-specific and are described elsewhere.<br>Parameters specified when running quick command override configured values. In case if a parameter is specified only for one header then<br>the value is multiplied for all the other headers (if required).<br>start  () Commands start the traffic generator tool in the background. It accepts one parameter  test-id<br>stop  () Command stops the started traffic generator tool by  start  command.<br>inject  () Inject raw data into the interface.<br>inject- Inject raw data directly from a PCAP or PCAPNG file.<br>pcap  ()<br>Starting with RouterOS 7.20, the sniffer tool saves captured packets in PCAPNG format.<br>The traffic-generator inject-pcap feature supports PCAPNG format starting from RouterOS 7.21.<br>**----- End of picture text -----**<br>
