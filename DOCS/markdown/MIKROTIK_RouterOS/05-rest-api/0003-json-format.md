## JSON format 

Server broadly follows ECMA-404 standard, with following notes: 

In JSON replies all object values are encoded as strings, even if the underlying data is a number or a boolean. 

227 

The server also accepts numbers in octal format (begins with 0) and hexadecimal format (begins with 0x). If the numbers are sent in a string format, they are assumed to be in decimal format. 

Numbers with exponents are not supported.
