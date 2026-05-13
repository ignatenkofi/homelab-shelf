## Proxy-based firewall – Access List 

An access list is implemented in the same way as MikroTik firewall rules processed from the top to the bottom. The first matching rule specifies the decision of what to do with this connection. Connections can be matched by their source address, destination address, destination port, sub-string of the requested URL (Uniform Resource Locator), or request method. If none of these parameters is specified, every connection will match this rule. 

If a connection is matched by a rule, the action property of this rule specifies whether a connection will be allowed or not (deny). If a connection does not match any rule, it will be allowed. 

In this example assume that we have configured a transparent proxy server, it will block the website http://www.facebook.com, we can always block the same for different networks by giving src-address: 

```
/ip proxy access add src-address=192.168.1.0/24 dst-host=www.facebook.com action=deny
```

Users from network 192.168.1.0/24 will not be able to access the website www.facebook.com. 

You can block also websites that contain specific words in the URL: 

931 

```
/ip proxy access add dst-host=:mail action=deny
```

This statement will block all websites which contain the word “mail” in the URL. Like www.mail.com, www.hotmail.com, mail.yahoo.com, etc. 

We can also stop downloading specific types of files like .flv, .avi, .mp4, .mp3, .exe, .dat, …etc. 

```
 /ip proxy access
 add path=*.flv action=deny
 add path=*.avi action=deny
 add path=*.mp4 action=deny
 add path=*.mp3 action=deny
 add path=*.zip action=deny
 add path=*.rar action=deny
```

Here are available also different wildcard characters, to create specific conditions and to match them by proxy access list. Wildcard properties (dst-host and dst-path) match a complete string (i.e., they will not match "example.com" if they are set to "example"). Available wildcards are '*' (match any number of any characters) and '?' (match any one character). 

Regular expressions are also accepted here, but if the property should be treated as a regular expression, it should start with a colon (':'). 

To show that no symbols are allowed before the given pattern, we use the ^ symbol at the beginning of the pattern. 

To specify that no symbols are allowed after the given pattern, we use the $ symbol at the end of the pattern.
