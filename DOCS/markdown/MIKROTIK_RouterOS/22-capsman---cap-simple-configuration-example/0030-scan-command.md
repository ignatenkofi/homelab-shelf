## Scan command 

The '/interface wifi scan' command will scan for access points and print out information about any APs it detects. 

The scan command takes all the same parameters as the frequency-scan command. 

Output parameters Parameter Description active (boolean) (A) This signifies that beacons from the AP have been received in the last 30 seconds. address (MAC) The MAC address (BSSID) of the AP. 

1361 

**==> picture [474 x 95] intentionally omitted <==**

**----- Start of picture text -----**<br>
channel  (string) The control channel frequency used by the AP, its supported wireless standards and control/extension channel layout.<br>security  (string) Authentication methods supported by the AP.<br>signal  (integer) The signal strength of the AP's beacons (in dBm).<br>ssid  (string) The extended service set identifier of the AP.<br>sta-count  (integer) The number of client devices associated with the AP. Only available if the AP includes this information in its beacons.<br>**----- End of picture text -----**<br>
