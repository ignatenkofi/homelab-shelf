## IPv6 connectivity 

WinBox supports IPv6 connectivity. To connect to the router's IPv6 address, it must be placed in square braces the same as in web browsers when connecting to the IPv6 server. Example: 

[db8::1] 

when connecting to the link-local address interface index must be entered after the %: 

[0:a00:27ff:fe70::e88c%2] 

Port number is set after the square brace when it is necessary to connect WinBox to other port than the default: 

[0:a00:27ff:fe70::e88c]:8299 

WinBox neighbor discovery is capable of discovering IPv6 enabled routers. There are two entries for each IPv6 enabled router, one entry is with IPv4 address and another one with IPv6 link-local address. You can easily choose which one you want to connect to.
