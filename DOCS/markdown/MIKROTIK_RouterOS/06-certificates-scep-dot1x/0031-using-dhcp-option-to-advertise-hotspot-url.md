## Using DHCP option to advertise HotSpot URL 

Most devices, such as modern smartphones, do some kind of background checking to see if they are behind a captive portal. They do this by requesting a known webpage and comparing the contents of that page, to what they should be. If contents are different, the device assumes there is a login page and creates a popup with this login page. 

This does not always happen, as this "known webpage" could be blocked, whitelisted, or not accessible in internal networks. To improve on this mechanism, RFC 7710 was created, allowing the HotSpot to inform all DHCP clients that they are behind a captive-portal device and that they will need to authenticate to get Internet access, regardless of what webpages they do or do not request. 

This DHCP option field is enabled automatically, but only if the router has a DNS name configured and has a valid SSL certificate (so that the login page can be accessed over HTTPS). When these requirements are met, a special DHCP option will be sent, containing a link to `https://<dns-name-ofhotspot>/api` . This link contains information in JSON format, instructing the client device of the captive portal status, and the location of the login page. 

Contents of `https://<dns-name-of-hotspot>/api` are as follows: 

```
{
"captive": $(if logged-in == 'yes')false$(else)true$(endif),
"user-portal-url": "$(link-login-only)",
$(if session-timeout-secs != 0)
"seconds-remaining": $(session-timeout-secs),
$(endif)
$(if remain-bytes-total)
"bytes-remaining": $(remain-bytes-total),
$(endif)
"can-extend-session": true
}
```

Some devices require venue-info URL as well, so you are free to modify the api.json file to your liking, just like any other hotspot files. It is located in the router files menu. 

**==> picture [13 x 13] intentionally omitted <==**
