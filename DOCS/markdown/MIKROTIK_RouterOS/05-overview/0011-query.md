## Query 

The ' `.query` ' key is used to create a query stack. The value is a list of query words. For example this POST request : 

```
POST https://router/rest/interface/print
{".query":["type=ether","type=vlan","#|!"]}
```

is equivalent to this API sentence 

```
/interface/print
?type=ether
?type=vlan
?#|!
```

For example, let's combine 'query' and 'proplist', to return '.id', 'address', and 'interface' properties for all dynamic records and records with the network 192.168.111.111 

```
$ curl -k -u admin: -X POST https://10.155.101.214/rest/ip/address/print \
```

```
  --data '{".proplist": [".id","address","interface"], ".query": ["network=192.168.111.111","dynamic=true","
#|"]}'\
```

- `-H "content-type: application/json"` 

```
[{".id":"*8","address":"10.155.101.214/24","interface":"sfp12"},
```

- `{".id":"*A","address":"192.168.111.111/32","interface":"dummy"}]`
