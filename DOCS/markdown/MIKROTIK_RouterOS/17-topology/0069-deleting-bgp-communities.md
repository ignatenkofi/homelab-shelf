## Deleting BGP Communities 

Routing filters allow to clear BGP communities by using "delete" command. Delete command accepts several parameters based on the type of the community type: 

communities : "wk" - will match and remove well known communities "other" - will match and remove other communities that are not well known "regexp" - regexp pattern to match communities that should be deleted "<community-list name>" - deletes communities from specified community-list ext-communities : "rt" - will match and remove RouteTarget "soo" - will match and remove Site-of-Origin "other" - will match and remove other ext communities that are not RT or SSO "regexp" - regexp pattern to match ext communities that should be deleted "<community-ext-list name>" - deletes communities from specified community-ext-list large-communities : "all" - removes everything "regexp" - regexp pattern to match large communities that should be deleted "<community-large-list name>" - deletes large communities from specified community-large-list 

It is possible to specify multiple community types, for example delete all SSOs, other type of ext communities and specific RTs from the community-ext list: 

```
/routing/filter/community-ext-list
add list=myRTList communities="rt:1.1.1.1:222"
/routing/filter/rule
add chain=myChain rule="delete bgp-ext-communities sso,other,myRTList;"
```
