## Introduction 

SOCKS (Socket Secure) is a proxy server that allows TCP-based application data to relay across the firewall, even if the firewall would block the packets. The SOCKS protocol is independent of application protocols, so it can be used for many services, e.g, WWW, FTP, TELNET, and others. 

At first, an application client connects to the SOCKS proxy server, then the proxy server looks in its access list to see whether the client is permitted to access the remote application resource or not, if it is permitted, the proxy server relies on the packet to the application server and creates a connection between the application server and client.
