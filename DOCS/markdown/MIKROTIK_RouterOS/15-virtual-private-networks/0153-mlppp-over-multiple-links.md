## MLPPP over multiple links 

MLPPP over multiple links allow to create a single PPP link over multiple physical connections. All PPP links must come from the same server (server must have MLPPP over multiple links support) and all PPP links must have same user name and password. 

And to enable MLPPP you just need to create PPP client and specify multiple interfaces instead of single interface. RouterOS has MLPPP client support only. Presently there are no MLPPP server support available. 

1258
