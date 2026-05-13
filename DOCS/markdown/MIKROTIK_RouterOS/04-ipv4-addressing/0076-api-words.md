## API words 

Words are part of a sentence. Each word has to be encoded in a certain way - the length of the word followed by the word content. The length of the word should be given as a count of bytes that are going to be sent. 

The length of the word is encoded as follows: 

**==> picture [286 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
Value of length # of bytes Encoding<br>0 <= len <= 0x7F 1 len, lowest byte<br>0x80 <= len <= 0x3FFF 2 len | 0x8000, two lower bytes<br>**----- End of picture text -----**<br>


195 

**==> picture [286 x 58] intentionally omitted <==**

**----- Start of picture text -----**<br>
0x4000 <= len <= 0x1FFFFF 3 len | 0xC00000, three lower bytes<br>0x200000 <= len <= 0xFFFFFFF 4 len | 0xE0000000<br>len >= 0x10000000 5 0xF0 and len as four bytes<br>**----- End of picture text -----**<br>


Each word is encoded as length, followed by that many bytes of content; 

- Words are grouped into sentences. The end of a sentence is terminated by a zero-length word; 

- The scheme allows encoding of length up to 0x7FFFFFFFFF , only four-byte length is supported; len bytes are sent most significant first (network order); 

- If the first byte of the word is >= 0xF8 , then it is a reserved control byte. After receiving an unknown control byte API client cannot proceed, because it does not know how to interpret the following bytes; 

Currently, control bytes are not used; 

In general, words can be described like this <<encoded word length><word content>>. Word content can be separated into 5 parts: command word, attribut e word, API attribute word. query word, and reply word
