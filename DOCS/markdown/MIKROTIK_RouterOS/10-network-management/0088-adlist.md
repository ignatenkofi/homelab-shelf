## Adlist 

Adlist is an integral component of network-level ad blocking, comprising a curated collection of domain names known for serving advertisements. This feature operates by utilizing Domain Name System (DNS) resolution to intercept A and AAAA requests to these domains. When a client device queries a DNS server for a domain listed on the adlist, the DNS resolution process is altered. Instead of returning the actual IP address of the ad-serving domain, the DNS server responds with the IP address 0.0.0.0. This effectively null-routes the request, as 0.0.0.0 is a non-routable meta-address used to denote an invalid, unknown, or non-applicable target. By redirecting ad-related requests in this manner, the adlist feature ensures that advertisement content is not loaded, enhancing network performance and improving the user experience by reducing unwanted ad traffic. 

Video: Adlist setup 

**==> picture [13 x 13] intentionally omitted <==**

Before configuring, increase the DNS cache as it's used to store adlist entries. If limit is reached and error in DNS,error topic is printed "adlist read: max cache size reached" 

**==> picture [13 x 13] intentionally omitted <==**

Adlist is stored on device's internal memory. Ensure that there is enough free space to save the desired adlist. 

920 

**==> picture [516 x 245] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>url Used to specify the URL of an adlist.<br>ssl-verify Specifies whether to validate the SSL certificate of the Adlist URL server.   Will use the "/certificate" list to verify server validity.<br>match- Count of matched DNS name requests.<br>count<br>name- Count of DNS names imported from the Adlist.<br>count<br>file Used to specify a local file path from which to read adlist data.<br>pause Temporarily pause the use of all adlist.<br>reload Checks for updates for all lists, if updates are found, the list is updated, removing or adding entries as needed, the lists are not<br>redownloaded in whole when issuing a reload, instead only necessary updates are done.<br>It's not mandatory to use reload to update the lists, Adlist checks for new updates once every four hours.<br>**----- End of picture text -----**<br>
