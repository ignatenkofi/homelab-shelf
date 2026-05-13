## RouterOS MAC-access 

RouterOS has built-in options for easy management access to network devices. The particular services should be shut down on production networks: MACTelnet, MAC-WinBox, and MAC-Ping: 

- `/tool mac-server set allowed-interface-list=none` 

- `/tool mac-server mac-winbox set allowed-interface-list=none` 

- `/tool mac-server ping set enabled=no`
