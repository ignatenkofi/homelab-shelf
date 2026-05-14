## MLPPP over single link 

Typically size of the packet sent over PPP link is reduced due to overhead. MP can be used to transmit and receive full frame over single ppp link. To make it work the Multilink Protocol uses additional LCP configuration options Multilink Maximum Received Reconstructed Unit (MRRU) 

To enable Multi-link PPP over single link you must specify MRRU (Maximum Receive Reconstructed Unit) option. If both sides support this feature there are no need for MSS adjustment (in firewall mangle). Study shows that MRRU is less CPU expensive that 2 mangle rules per client. MRRU allows to divide packet to multiple channels therefore increasing possible MTU and MRU (up to 65535 bytes) 

Under Windows it can be enabled in Networking tag, Settings button, "Negotiate multi-link for single link connections". Their MRRU is hard coded to 1614. 

**==> picture [13 x 13] intentionally omitted <==**

MTU will be reduced by 4 bytes to work properly when MPPE encryption is enabled
