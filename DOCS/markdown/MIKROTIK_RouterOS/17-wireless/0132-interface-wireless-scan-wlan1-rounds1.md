## `/interface wireless scan wlan1 rounds=1` 

'save-file' option allows to do scripted/scheduled scans and save the results in file for future analysis. Also this feature together with rounds setting allows to get scan results from the remote wireless clients - executing that command will start the scan tool which disconnect the wireless link, does the scan through the scan-list frequencies and saves the results to file, exits the scan and connects the wireless link back. Example:
