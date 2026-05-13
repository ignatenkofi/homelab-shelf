## Supported Operators 

**==> picture [516 x 176] intentionally omitted <==**

**----- Start of picture text -----**<br>
Operator Description Example Example Explained Example<br>Matches<br>^ Represents the beginning of the path ^1234  will match AS-path starting with ASN 1234<br>$ Represents the end of the path 1234$ will match AS-path of origin ASN 1234<br>* Zero or more occurrences of the  listed ASN ^1234*$ will match Null as-path or as-path where ASN 1234 may or  Match:<br>may not appear multiple times<br>1234<br>1234 1234<br>1234<br>Null path<br>No Match:<br>1234 5678<br>**----- End of picture text -----**<br>


1061 

**==> picture [516 x 571] intentionally omitted <==**

**----- Start of picture text -----**<br>
+ One or more occurrences of the listed ASN 1234+ will match AS-path where ASN 1234 appears at least once Match:<br>1234<br>3 1234 6<br>No match:<br>12345 678<br>? Zero or one occurrence of the listed ASN ^1234?  will match AS-path that may or may not start with ASN  Match :<br>5678 1234 appearing once.<br>5678<br>1234 5678<br>No match:<br>1234 1234<br>5678<br>12345 5678<br>. One occurrence of any ASN ^.$  will match any AS-path with the length of one. Match:<br>12345<br>45678<br>No match:<br>1234 5678<br>| Match one of two ASNs on each side ^ will match AS-path starting with ASN 1234 or 5678 Match :<br>(1234|5678)<br>1234<br>5678<br>1234 5678<br>No Match:<br>91011<br>[ ] Represents the set of AS numbers where one AS number  ^[1234  will match the AS-path that starts with 1234 or 5678 or from  Match:<br>from the list must match. 5678 1-100] the range of 1 to 100<br>[^ ] 1234<br>Use ^ after opening the bracket to negate the set.<br>99<br>It is also possible to reference the pre-defined num-lists from n<br>um-list with [[:numset_name:]]  5678<br>No Match:<br>101<br>() Group of regexp terms to match ^ will match AS-path that starts and ends with 1234 or AS- Match:<br>(1234$|567 path that starts with 5678<br>8) 1234<br>5678 9999<br>No Match:<br>1234 5678<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Repetition ranges {} are not supported.
