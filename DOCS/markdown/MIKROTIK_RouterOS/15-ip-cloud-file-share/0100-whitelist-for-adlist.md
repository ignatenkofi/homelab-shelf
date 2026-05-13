## Whitelist for Adlist 

To exempt certain domains from Adlist, you need to create a static DNS FWD entry, for example, `/ip/dns/static/add name=bar.test type=FWD` , if such entry is present, the query will be forwarded to the next DNS, either dynamic or one configured under " `/ip/dns/set servers=` " , FWD entries are supported by DoH as well.
