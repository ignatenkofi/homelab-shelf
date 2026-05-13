## VLAN Forwarding 

Both `vlan-mode` and `vlan-header` along with the VLAN Table can be used to configure VLAN tagging, untagging and filtering, multiple combinations are possible, each achieving a different result. Below you can find a table of what kind of traffic is going to be sent out through an egress port when a certain traffic is received on an ingress port for each VLAN Mode. 

NOTES: 

- L - `vlan-header` is set to `leave-as-is` S - `vlan-header` set to `always-strip` 

- A - `vlan-header` set to `add-if-missing` 

- U - Untagged traffic is sent out 

- T - Tagged traffic is sent out, a tag is already present on the ingress port TA - Tagged traffic is sent out, a tag was added on the ingress port 

- DI - Traffic is dropped on ingress port because of mode selected in vlan-mode 

484 

DE - Traffic is dropped on egress port because egress port was not found in the VLAN Table VID match - VLAN ID from the VLAN tag for ingress traffic is present in the VLAN Table Port match - Ingress port is present in the VLAN Table for the appropriate VLAN ID 

**==> picture [397 x 523] intentionally omitted <==**

**----- Start of picture text -----**<br>
VLAN Mode = disabled Egress port not present in VLAN Table Egress port is present in VLAN Table<br>L S A L S A<br>Untagged traffic U U TA U U TA<br>Tagged traffic; no VID match T U T<br>Tagged traffic; VID match; no Port match T U T T U T<br>Tagged traffic; VID match; Port match T U T T U T<br>VLAN Mode = fallback Egress port not present in VLAN Table Egress port is present in VLAN Table<br>L S A L S A<br>Untagged traffic U U TA U U TA<br>Tagged traffic; no VID match T U T<br>Tagged traffic; VID match; no Port match DE DE DE T U T<br>Tagged traffic; VID match; Port match DE DE DE T U T<br>VLAN Mode = check Egress port not present in VLAN Table Egress port is present in VLAN Table<br>L S A L S A<br>Untagged traffic<br>Tagged traffic; no VID match DI DI DI<br>Tagged traffic; VID match; no Port match DE DE DE T U T<br>Tagged traffic; VID match; Port match DE DE DE T U T<br>VLAN Mode = secure Egress port not present in VLAN Table Egress port is present in VLAN Table<br>L S A L S A<br>Untagged traffic<br>Tagged traffic; no VID match DI DI DI<br>Tagged traffic; VID match; no Port match DI DI DI DI DI DI<br>Tagged traffic; VID match; Port match DE DE DE T U T<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

The tables above are meant for more advanced configurations and to double-check your understanding of how packets will be processed with each VLAN related property.
