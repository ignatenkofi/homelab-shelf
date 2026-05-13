## RouterOS /32 and IP unnumbered addresses 

In RouterOS, to create a point-to-point tunnel with addresses you have to use the address with a network mask of '/32' that effectively brings you the same features as some vendors unnumbered IP address. 

There are 2 routers RouterA and RouterB where each is part of networks 10.22.0.0/24 and 10.23.0.0/24 respectively and to connect these routers using VLANs as a carrier with the following configuration:
