## Proplist 

The '. `proplist` ' key is used to create `.proplist` attribute word. The values can be a single string with comma-separated values: 

229 

```
POST https://router/rest/interface/print
{".proplist":"name,type"}
```

or a list of strings: 

```
POST https://router/rest/interface/print
{".proplist":["name","type"]}
```

For example, return address and interface properties from the ip/address list: 

```
$ curl -k -u admin: -X POST https://10.155.101.214/rest/ip/address/print\
  --data '{"_proplist": ["address","interface"]}' -H "content-type: application/json"
[{"address":"192.168.99.2/24","interface":"dummy"},
{"address":"172.16.5.1/24","interface":"sfpplus1"},
{"address":"172.16.6.1/24","interface":"sfp2"},
{"address":"172.16.7.1/24","interface":"sfp3"},
{"address":"10.155.101.214/24","interface":"sfp12"},
{"address":"192.168.111.111/32","interface":"dummy"}]
```
