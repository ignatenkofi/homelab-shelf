## RouterOS LPA supports: 

AT modems which firmware supports SIM low access commands (AT+CCHO; AT+CCHC; AT+CGLA) MBIM modems which supports SIM low level access service in its firmware (UUID_SERVICE_MS_UICC) 

Other requirements: 

eSIM in SIM cards form factor (physical eSIM) inserted in RouterBoard SIM slot 

eSIM/eUICC present on modem (soldered chip) and modem set to use this slot 

connectivity to eSIM SIM profile provider SM-DP+ provisioning server during provisioning and deletion of SIM profiles on eSIM chip (for connectivity, can use another eSIM profile or another WAN interface) 

eSIM can be provisioned only if the active slot is eSIM 

Some devices have multiple SIM slots, and to use an eSIM, you need to switch the slot using the command "/interface lte settings set simslot=esim". 

Command **`/interface/lte/esim esim-id [find /interface/lte]`** can be used to check whether the modem supports SIM low access commands and eSIM presence. 

If 3rd party modem with embedded eSIM chip is used, please consult modem manual regarding AT commands needed to select eSIM slot (AT!UIMS; AT+QUIMSLOT etc).
