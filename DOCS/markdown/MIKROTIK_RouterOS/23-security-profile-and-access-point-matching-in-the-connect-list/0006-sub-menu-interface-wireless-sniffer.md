## Sub-menu: `/interface wireless sniffer` 

Wireless sniffer allows to capture frames including Radio header, 802.11 header and other wireless related information. 

**==> picture [504 x 264] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>channel-time  (; Default: 200ms ) How long to sniff each channel. Used only if  multiple-channels=yes<br>file-limit  (integer [10..4294967295]; Default: Allocated file size in bytes which will be used to store captured data. Applicable if file-name is<br>10 ) specified.<br>file-name  (string; Default: ) Name of the file where to store captured data.<br>memory-limit  (integer [10..4294967295];  Allocated memory buffer in kilobytes used to store captured data.<br>Default: 10 )<br>multiple-channels  (yes | no; Default: no ) Whether to sniff multiple channels or a single channel.  No  means that all channel settings will be<br>taken from  /interface wireless ,<br>Yes  means that all channel settings will be taken from  scan-list  under  /interface wireless .<br>only-headers  (yes | no; Default: no ) If set to yes, then sniffer will capture only information stored in frame headers.<br>receive-errors  (yes | no; Default: no ) Whether to process packets which have been received with errors judging by their FCS.<br>streaming-enabled  (yes | no; Default: no ) Whether to stream captured data to the specified streaming server<br>streaming-max-rate  (integer [0..4294967295] Maximum packets per second allowed.  equals unlimited 0<br>; Default: 0 )<br>streaming-server  (IPv4; Default: 0.0.0.0 ) IP address of the streaming server.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Use the command /interface wireless info scan-list to verify your scan-list defined under /interface wireless channels when using multiplechannels=yes
