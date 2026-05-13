## Overview 

CAPsMAN allows applying wireless settings to multiple MikroTik AP devices from a central configuration interface. 

More specifically, the Controlled Access Point system Manager (CAPsMAN) allows centralization of wireless network management and if necessary, data processing. When using the CAPsMAN feature, the network will consist of a number of 'Controlled Access Points' (CAP) that provide wireless connectivity and a 'system Manager' (CAPsMAN) that manages the configuration of the APs, it also takes care of client authentication and optionally, data forwarding. 

When a CAP is controlled by CAPsMAN it only requires the minimum configuration required to allow it to establish a connection with CAPsMAN. Functions that were conventionally executed by an AP (like access control, client authentication) are now executed by CAPsMAN. The CAP device now only has to provide the wireless link layer encryption/decryption. 

Depending on the configuration, data is either forwarded to CAPsMAN for centralized processing (default) or forwarded locally at the CAP itself (local forwarding mode). 

Requirements 

- Any RouterOS device can be a controlled wireless access point (CAP) as long as it has at least a Level 4 RouterOS license CAPsMAN server can be installed on any RouterOS device, even if the device itself does not have a wireless interface Unlimited CAPs (access points) supported by CAPsMAN 

- 32 Radios per CAP maximum 

- 32 Virtual interfaces per master radio interface maximum 

- Not possible to use Nv2 and NStreme proprietary protocols
