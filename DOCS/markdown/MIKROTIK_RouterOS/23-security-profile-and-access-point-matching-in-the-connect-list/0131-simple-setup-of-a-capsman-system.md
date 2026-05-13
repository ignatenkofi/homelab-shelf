## Simple setup of a CAPsMAN system 

1472 

**==> picture [504 x 358] intentionally omitted <==**

Before deep-diving into the details of CAPsMAN operation, let us quickly illustrate how to set up the most basic system where you have a MikroTik router that manages two MikroTik AP devices. The benefit of CAPsMAN is that the CAP units don't need to be configured, all settings are done in the CAPsMAN server. 

The CAPsMAN setup consists of defining configuration templates, which will then be pushed to the controllable AP devices (CAPs). Assuming your main router is already connected to the internet and works fine, you can proceed as follows. 

In the central device, which will be your CAPsMAN server, create a new "Configuration" template with only the basic settings (network name, country, the local LAN bridge interface, the wireless password): 

1473 

**==> picture [505 x 286] intentionally omitted <==**

1. 

2. 

add new configuration profile 

**==> picture [505 x 342] intentionally omitted <==**

1474 

3. 

**==> picture [505 x 291] intentionally omitted <==**

Then create a new "Provisioning" rule, which will assign the created configuration template to the CAP devices: 

4. 

**==> picture [505 x 221] intentionally omitted <==**

All that remains to do on the CAPsMAN, is to enable it: 

1475 

5. 

**==> picture [505 x 216] intentionally omitted <==**

Most MikroTik AP devices already support CAP mode out of the box, all you need to do, is make sure they are on the same network as your CAPsMAN, and then boot them up, while holding the reset button. 

So, for example, connect the CAP device to one of the CAPsMAN device LAN ports while it is turned off, then hold the reset button, and power on the CAP device. Keep holding the button until the User LED turns solid, release now to turn on CAP mode. The device will now look for a CAPsMAN server (total time to hold the button, around 10 seconds). 

The device will now show up in the CAPsMAN "Remote CAP" menu and will be "provisioned" with the configuration template, as per the provisioning settings. For more details on how to manually adjust all settings, keep reading this document.
