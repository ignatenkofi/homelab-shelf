## Attribute word 

Each command word has its list of attribute words depending on content. 

Attribute word structure consists of 5 parts in this order: 

encoded length content prefix equals sign - = attribute name separating equals sign - = value of an attribute if there is one. It is possible that the attribute does not have a value 

**==> picture [13 x 13] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

Value can hold multiple equal signs in the value of an attribute word since the way the word is encoded. Value can be empty. 

Examples without encoded length prefix: 

196 

```
=address=10.0.0.1
```

```
=name=iu=c3Eeg
```

```
=disable-running-check=yes
```

**==> picture [13 x 12] intentionally omitted <==**

Order of attribute words and API parameters is not important and should not be relied on
