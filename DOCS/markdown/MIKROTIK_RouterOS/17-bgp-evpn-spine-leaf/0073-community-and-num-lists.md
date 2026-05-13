## Community and Num Lists 

A list of commonly used numbers can be configured from the `/routing/filter/num-list` menu. These lists of numbers can be used in the filter rules to simplify the filter setup process. 

1062 

In a similar manner, you are allowed to define also community, extended community, and large community lists. Community sets can be used for matching, appending, and setting. 

For example match communities from the list and clear the attribute: 

```
/routing/filter/community-list
add communities=111:222 list=myCommunityList
```

```
/routing/filter/rule
```

```
add chain=myChain rule="if (bgp-communities equal-list myCommunityList) {delete bgp-communities wk,other;
accept;}"
```
