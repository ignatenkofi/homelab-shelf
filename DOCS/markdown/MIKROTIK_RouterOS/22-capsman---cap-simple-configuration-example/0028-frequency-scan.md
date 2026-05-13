## Frequency scan 

Information about RF conditions on available channels can be obtained by running the frequency-scan command. 

Command parameters Parameter Description duration (time interval; default: none ) Length of time to perform the scan for before exiting. Useful for non-interactive use. freeze-frame-interval (time interval; Time interval at which to update command output. default: 1s ) 

1360 

frequency (list of frequencies/ranges) Frequencies to perform the scan on. See channel.frequency parameter syntax above for more detail. Defaults to all supported frequencies. number (string; default: none ) Either the name or internal id of the interface to perform the scan with. Required. rounds (integer; default: none ) Number of times to go through list of scannable frequencies before exiting. Useful for non-interactive use. save-file (string; default: none ) Name of file to save output to. 

**==> picture [318 x 196] intentionally omitted <==**

**----- Start of picture text -----**<br>
Output parameters<br>Parameter Description<br>channel  (integer) Frequency (in MHz) of the channel scanned.<br>networks  (integer) Number of access points detected on the channel.<br>load  (integer) Percentage of time the channel was busy during the scan.<br>nf  (integer) Noise floor (in dBm) of the channel.<br>max-signal  (integer) Maximum signal strength (in dBm) of APs detected in the channel.<br>min-signal  (integer) Minimum signal strength (in dBm) of APs detected in the channel.<br>primary  (boolean) (P) Channel is in use as the primary (control) channel by an AP.<br>secondary  (boolean) (S) Channel is in use as a secondary (extension) channel by an AP.<br>**----- End of picture text -----**<br>
