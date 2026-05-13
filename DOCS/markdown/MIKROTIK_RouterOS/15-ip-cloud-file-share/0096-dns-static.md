## DNS Static 

The MikroTik RouterOS DNS cache has an additional embedded DNS server feature that allows you to configure multiple types of DNS entries that can be used by the DNS clients using the router as their DNS server. This feature can also be used to provide false DNS information to your network clients. For example, resolving any DNS request for a certain set of domains (or for the whole Internet) to your own page. 

```
[admin@MikroTik] /ip dns static add name=www.mikrotik.com address=10.0.0.1
```

The server is also capable of resolving DNS requests based on basic regular expressions so that multiple requests can be matched with the same entry. In case an entry does not conform with DNS naming standards, it is considered a regular expression. The list is ordered and checked from top to bottom. Regular expressions are checked first, then the plain records. 

Use regex to match DNS requests: 

```
[admin@MikroTik] /ip dns static add regexp="[*mikrotik*]" address=10.0.0.2
```

If DNS static entries list matches the requested domain name, then the router will assume that this router is responsible for any type of DNS request for the particular name. For example, if there is only an "A" record in the list, but the router receives an "AAAA" request, then it will reply with an "A" record from the static list and will query the upstream server for the "AAAA" record. If a record exists, then the reply will be forwarded, if not, then the router will reply with an "ok" DNS reply without any records in it. If you want to override domain name records from the upstream server with unusable records, then you can, for example, add a static entry for the particular domain name and specify a dummy IPv6 address for it "::ffff". 

List all of the configured DNS entries as an ordered list: 

```
[admin@MikroTik] /ip/dns/static/print
Columns: NAME, REGEXP, ADDRESS, TTL
# NAME             REGEXP       ADDRESS   TTL
0 www.mikrotik.com               10.0.0.1  1d
1                  [*mikrotik*]  10.0.0.2  1d
```

**==> picture [516 x 174] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IPv4/IPv6) The address that will be used for "A" or "AAAA" type records.<br>cname  (string) Alias name for a domain name.<br>forward-to The IP address of a domain name server to which a particular DNS request must be forwarded.<br>mx-exchange  (string) The domain name of the MX server.<br>name  (string) Domain name.<br>srv-port  (integer; Default: )0 The TCP or UDP port on which the service is to be found.<br>srv-target The canonical hostname of the machine providing the service ends in a dot.<br>text  (string) Textual information about the domain name.<br>**----- End of picture text -----**<br>


918 

type (A  | AAAA | CNAME | FWD | MX | NS | N Type of the DNS record. XDOMAIN | SRV | TXT ; Default: A) 

**==> picture [516 x 200] intentionally omitted <==**

**----- Start of picture text -----**<br>
address-list  (string) Name of the Firewall address list to which address must be dynamically added when some request<br>matches the entry. Entry will be removed from the address list when TTL expires.<br>comment  (string) Comment about the domain name record.<br>disabled  (yes  no| ; Default: yes) Whether the DNS record is active.<br>match-subdomain  (yes  no| ; Default: no) Whether the record will match requests for subdomains.<br>mx-preference  (integer; Default: 0) Preference of the particular MX record.<br>ns  (string) Name of the authoritative domain name server for the particular record.<br>regexp  (regex) Regular expression against which domain names should be verified.<br>srv-priority  (integer; Default: 0) Priority of the particular SRV record.<br>srv-weight  (integer; Default: )0 Weight of the particular SRV record.<br>ttl  (time; Default: 24h) Maximum time-to-live for cached records.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

For each static A and AAAA record, in cache automatically is added a PTR record. 

**==> picture [13 x 13] intentionally omitted <==**

Regexp is case-sensitive, but DNS requests are not case sensitive, RouterOS converts DNS names to lowercase before matching any static entries. You should write regex only with lowercase letters. Regular expression matching is significantly slower than plain text entries, so it is advised to minimize the number of regular expression rules and optimize the expressions themselves. 

**==> picture [13 x 13] intentionally omitted <==**

Be careful when you configure regex through mixed user interfaces - CLI and GUI. Adding the entry itself might require escape characters when added from CLI. It is recommended to add an entry and the execute print command in order to verify that regex was not changed during addition.
