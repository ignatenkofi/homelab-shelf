## Arithmetic Operators 

Usual arithmetic operators are supported in the RouterOS scripting language 

**==> picture [255 x 136] intentionally omitted <==**

**----- Start of picture text -----**<br>
Operator Description Example<br>"+" binary addition :put (3+4);<br>"-" binary subtraction :put (1-6);<br>"*" binary multiplication :put (4*5);<br>"/" binary division :put (10 / 2); :put ((10)/2)<br>"%" modulo operation :put (5 % 3);<br>"-" unary negation { :local a 1; :put (-a); }<br>**----- End of picture text -----**<br>

Note: for the division to work you have to use braces or spaces around the dividend so it is not mistaken as an IP address
