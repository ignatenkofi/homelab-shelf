## API sentences 

API sentence is the main object of communication using API. 

Empty sentences are ignored. 

A sentence is processed after receiving zero length word. 

- There is a limit on the number and size of sentences that the client can send before it has logged in. Order of attribute words should not be relied on. As order and count are changeable by .proplist attribute. The sentence structure is as follows: 

197 

The first word should contain a command word; Should contain zero-length word to terminate the sentence; Can contain none or several attribute words. There is no particular order in what attribute words have to be sent in the sentence, order is not important for attribute words; Can contain none or several query words. The order of query words in the sentence is important. 

**==> picture [13 x 13] intentionally omitted <==**

Zero-length word terminates the sentence. If it is not provided router will not start to evaluate sent words and will consider all the input as part of the same sentence.
