## RouterOS package type 

Since RouterOS v7.13 some MikroTik devices can choose between two types of Wireless NPK package (ie. wireless drivers), depending on the required features and the device type. More details can be found in the respective documentation sections. CAPsMAN functionality is included in the routeros bundle package, regardless of CPU architecture and independent of wireless drivers, ie. you can run CAPsMAN on any model. 

In short: 

CAPsMAN can run anywhere, on any MikroTik device. You can run both new and old CAPsMAN at the same time in most cases (when running both on an AX router, built in cards can't be used) 

MIPS type devices have no choice of driver, only legacy drivers are supported 

ARM CPU 802.11AC wireless devices has a choice of wireless driver: wireless.npk or wifi-qcom-ac.npk 

The below table helps you choose in this case:
