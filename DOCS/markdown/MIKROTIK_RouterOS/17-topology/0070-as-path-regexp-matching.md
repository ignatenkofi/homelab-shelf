## AS-PATH Regexp Matching 

AS Path is the sequence of autonomous system numbers (ASNs), for example AS Path 123 456 789 would indicate, that route originated from AS with the number 789, and to reach the destination, the packet would need to travel through two autonomous systems: 456 and 789. To apply specific routing policies administrator might want to match specific AS numbers or set of numbers in the AS Path (for example, reject prefixes that travel through AS 456), which can be achieved using regular expression (regexp). 

There are two common ways how to operate with AS Path data: 

convert whole AS path to string and let regexp operate on the string (ROS v6 or Cisco style) let regexp operate on each entry in the AS path as a number (ROS v7, Juniper style) 

Basically, the first method is performing the match per character, the second method is performing the match per whole AS number. As you would imagine the latter method is much faster and less resource-intensive than the string matching approach. 

1060 

This change would require administrators to implement new Regex strategies. Old Regex patterns from RouterOS v6 cannot be directly copied/pasted as they will result either in syntax errors or unexpected results. 

Let us take a very basic AS Path filter rule. 

```
/routing/filter/rule
```

```
add chain=myChain rule="if (bgp-as-path .1234.) {accept}"
```

In ROS v7 this Regex pattern will match ASN 1234 anywhere in the middle of the AS-path, the same pattern in ROS v6 would match any AS path that contains ASN consisting of at least 6 characters and contains a string of "1234".  Obviously, if we directly copy/paste the Regex pattern from one implementation to another it will lead to unexpected/dangerous results. An equivalent pattern in ROS v6 would look something like this: "._1234_.". 

Let's take another example from ROS v6, say we have a pattern "1234[5-9]" what it does is it matches 12345 to 12349 anywhere in the string, which means that valid matches are AS-path "12345 3434", "11 9123467 22" and so on. If you enter the same pattern in ROS v7 it will match AS path containing exact ASN 1234 followed by ASN in a range from 5 to 9 (matching AS-paths would be "1234 7 111", "111 1234 5 222" etc., it will not match "12345 3434"). 

**==> picture [13 x 13] intentionally omitted <==**

Do not copy Regex patterns directly from ROS v6 or Cisco configurations, they are not directly compatible. It can lead to unexpected or even dangerous configurations in some scenarios. 

**==> picture [13 x 13] intentionally omitted <==**

AS-Path parameter must exist for regexp matcher to be applied. This means that it is not possible to match non-existent (empty) AS-Path with regular expression, aka "^$". `bgp-path-len` should be used instead.
