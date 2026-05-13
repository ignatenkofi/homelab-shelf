## `# Older RouterOS` 

```
/interface ethernet set sfp-sfpplus1 auto-negotiation=no speed=1Gbps full-duplex=yes
```

auto-negotiation disabled port speed 1G full-duplex 

Devices which SFP+ ports support 1G links: 

- CCR2004-1G-12S+2XS - All SFP+ interfaces can be used in 1G mode if required. CCR2004-16G-2S+ - All SFP+ interfaces can be used in 1G mode if required. CCR1072-1G-8S+ - All SFP+ interfaces can be used in 1G mode if required. CCR1036-8G-2S+ - All SFP+ interfaces can be used in 1G mode if required. CCR1009-8G-1S-1S+ - All SFP+ interfaces can be used in 1G mode if required. CCR1009-7G-1C-1S+ - All SFP+ interfaces can be used in 1G mode if required. CSS3xx series switches - All SFP+ interfaces can be used in 1G mode if required. CRS3xx series switches - All SFP+ interfaces can be used in 1G mode if required. RB5009 series - SFP+1 interface can be used in 1G mode if required. RB4011 series - SFP+1 interface can be used in 1G mode if required. CRS226-24G-2S+ - Only SFP+1 supports 1G link speed, SFP+2 is for 10G links only. CRS210-8G-2S+ - Only SFP+1 supports 1G link speed, SFP+2 is for 10G links only. CSS610 series switches - All SFP+ interfaces can be used in 1G mode if required. FTC11XG - SFP+1 interface can be used in 1G mode if required. 

Devices which SFP+ interfaces can be used only for 10G links: 

CCR1016-12S-1S+ 

CRS212-1G-10S-1S+
