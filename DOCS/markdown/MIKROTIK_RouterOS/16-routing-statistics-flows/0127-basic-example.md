## Basic Example 

Let's consider that we have our own RTR server on our network with IP address 192.168.1.1: 

```
/routing/bgp/rpki
```

```
add group=myRpkiGroup address=192.168.1.1 port=8282 refresh-interval=20
```

If the connection is established and a database from the validator is received, we can check prefix validity: 

```
[admin@rack1_b33_CCR1036] /routing> rpki-check group=myRpkiGroup prfx=70.132.18.0/24 origin-as=16509
    valid
```

Now the cached database can be used by routing filters to accept/reject prefixes based on RPKI validity. At first, we need to set up a filter rule which defines against which RPKI group performs the verification. After that filters are ready to match the status from the RPKI database. Status can have one of three values: 

valid - database has a record and origin AS is valid. 

invalid - the database has a record and origin AS is invalid. 

unknown - database does not have information of prefix and origin AS. 

unverified - set when none of the RPKI sessions of the RPKI group has synced database. This value can be used to handle the total failure of the RPKI. 

```
/routing/filter/rule
add chain=bgp_in rule="rpki-verify myRpkiGroup"
add chain=bgp_in rule="if (rpki invalid) { reject } else { accept }"
```

1016
