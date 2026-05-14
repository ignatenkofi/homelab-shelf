## Boards with USB-A port and mPCIe 

Some devices such as specific RB9xx's and the RBLtAP-2HnD share the same USB lines between a single mPCIe slot and a USB-A port. If auto switch is not taking place and a modem is not getting detected, you might need to switch manually to either use the USB-A or mini-PCIe: 

```
/system routerboard usb set type=mini-PCIe
```
