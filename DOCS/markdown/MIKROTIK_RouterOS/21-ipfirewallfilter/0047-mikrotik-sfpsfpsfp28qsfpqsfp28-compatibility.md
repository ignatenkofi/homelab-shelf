## MikroTik SFP/SFP+/SFP28/QSFP+/QSFP28 compatibility 

This article shows the compatibility of MikroTik devices with SFP, SFP+, SFP28, QSFP+, and QSFP28 transceivers. It features detailed compatibility tables that provide valuable insights into which transceivers are suitable for use with MikroTik devices. Additionally, some practical configuration examples are provided using the RouterOS CLI to set different data transmission rates. For more detailed descriptions of properties, please refer to the Ethernet user manual. 

**==> picture [13 x 13] intentionally omitted <==**

MikroTik devices and SFP, SFP+, SFP28, QSFP+, and QSFP28 modules do not have any restrictions for other vendor equipment. 

While MikroTik cannot ensure full compatibility with modules from all manufacturers, as long as the other vendor modules and devices comply with transceiver multi-source agreement (MSA) they should be compatible with MikroTik. 

**==> picture [13 x 13] intentionally omitted <==**

RouterOS uses a disabled FEC mode as the default setting for SFP28 and QSFP28 interfaces. To ensure a successful link with other vendor devices, you may need to enable FEC mode by configuring it to either `fec74` or `fec91` . For more information please refer to the Ethernet user manual.
