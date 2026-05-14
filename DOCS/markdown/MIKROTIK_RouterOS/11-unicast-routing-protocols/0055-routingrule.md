## /routing/rule 

List of all the parameters that can be used by routing rules: 

**==> picture [516 x 291] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (drop | lookup | lookup-only-in-table  An action to take on the matching packet:<br>| unreachable)<br>drop - silently drop the packet.<br>lookup - perform a lookup in routing tables.<br>lookup-only-in-table - perform lookup only in the specified routing table (see table parameter).<br>unreachable - generate ICMP unreachable message and send it back to the source.<br>comment  (string)<br>disabled  (yes | no) The disabled rule is not used.<br>dst-address () The destination address of the packet to match.<br>interface  (string) Incoming interface to match.<br>min-prefix  (integer [0..4294967295]) Routes from the routing table with specified prefix length is hidden to packets processed by routing rule.<br>Equivalent to Linux IP rule  suppress_prefixlength  . For example to suppress the default route in the<br>routing decision set the value to 0.<br>routing-mark  (string) Match specific routing mark.<br>src-address  (string) The source address of the packet to match.<br>table  (name) Name of the routing table to use for lookup.<br>**----- End of picture text -----**<br>

987
