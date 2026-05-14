## Label Range and TTL 

From the `/mpls settings` menu it is possible to assign specific dynamic label range and TTL propagation. If for some reason static label mapping is used then the dynamic range can be adjusted to exclude statically assigned label numbers from being dynamically assigned by any of the label distribution protocols. 

**==> picture [516 x 122] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>dynamic-label-range  (range of  Range of Label numbers used for dynamic allocation. The first 16 labels are reserved for special purposes (as defined<br>integer[16..1048575]; Default: in RFC). If you intend to configure labels statically then adjust the dynamic default range not to include numbers that<br>16-1048575 ) will be used in a static configuration.<br>propagate-ttl  (yes | no; Default: Whether to copy TTL values from IP header to MPLS header. If this option is set to no then hops inside the MPLS<br>yes ) cloud will be invisible from traceroutes.<br>allow-fast-path( yes | no;  Enable/disable MPLS fast-path support.<br>Default:  yes)<br>**----- End of picture text -----**<br>
