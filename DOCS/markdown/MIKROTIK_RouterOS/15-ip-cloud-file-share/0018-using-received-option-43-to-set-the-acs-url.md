## Using received Option 43 to set the ACS URL 

It is possible to set Automatic Configuration Server (ACS) URL in the TR069 client settings, when a DHCP client lease is bound, if the option sent from the DHCP server is configured to send it. Here's an example: 

```
:if ($bound=1) do={
/tr069-client/set acs-url=$"vendor-specific"
}
```
