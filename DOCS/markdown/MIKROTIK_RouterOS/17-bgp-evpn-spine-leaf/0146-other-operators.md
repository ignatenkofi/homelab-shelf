## Other Operators 

**==> picture [509 x 177] intentionally omitted <==**

**----- Start of picture text -----**<br>
Operator Description Example<br>“[]” command substitution. Can contain only a single command line :put [ :len "my test string"; ];<br>“()” subexpression or grouping operator :put ( "value is " . (4+5));<br>“$” substitution operator :global a 5; :put $a;<br>“~” the binary operator that matches value against POSIX extended regular  Print all routes whose gateway ends with 202:<br>expression /ip route print where gateway~"^[0-9 \\.]<br>*202\$"<br>“->” Get an array element by key [admin@x86] >:global aaa {a=1;b=2}<br>[admin@x86] > :put ($aaa->"a")<br>1<br>[admin@x86] > :put ($aaa->"b")<br>2<br>**----- End of picture text -----**<br>
