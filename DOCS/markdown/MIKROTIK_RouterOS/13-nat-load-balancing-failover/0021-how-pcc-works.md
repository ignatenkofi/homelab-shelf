## How PCC works 

This article aims to explain in simple terms how PCC works. The definition from the official manual wiki page reads: "PCC takes selected fields from IP header, and with the help of a hashing algorithm converts selected fields into 32-bit value. This value then is divided by a specified Denominator and the remainder then is compared to a specified Remainder, if equal then packet will be captured. You can choose from src-address, dst-address, src-port, dstport from the header to use in this operation.", with the full number of fields available being: "both-addresses|both-ports|dst-address-and-port|srcaddress|src-port|both-addresses-and-ports|dst-address|dst-port|src-address-and-port". If you understand that definition, there'll be nothing interesting in this article for you. 

First, here are the terms necessary to understand the definition. 

IP packets have a header that contains several fields, two of those fields are the IP address of the source of the packet and the IP address of the destination of the packet. TCP and UDP packets also have headers that contain the source port and the destination port. 

Denominators and remainders are parts of modulus operations. A modulus operation produces the integer left over when you divide two numbers and only accept the whole number portion of the result. It is represented by a % sign. Here are some examples: 3 % 3 = 0, because 3 divides cleanly by 3. 4 % 3 = 1, because the next smallest number to 4 that cleanly divides by 3 is 3, and 4 - 3 = 1. 5 % 3 is 2, because the next smallest number to 5 that divides cleanly by 3 is 3, and 5 - 3 = 2. 6 % 3 = 0, because 6 divides cleanly by 3. 

760 

A hash is a function that is fed input, and produces output. Hashes have many interesting properties, but the only important one for the purpose of this article is that hash functions are deterministic. That means that when you feed a hash function an input that reads 'hello' and it produces the output '1', you can rely on the fact that if you feed it 'hello' a second time it will produce the output '1' again. When you feed a hash function the same input, it will always produce the same output. What exact hashing algorithm is used by PCC is not important, so for this discussion let's assume that when you feed it IP addresses and ports, it just adds up the octets of the IP addresses as decimal numbers as well as the ports, and then takes the last digit and produces it as the output. Here an example: 

The hash function is fed 1.1.1.1 as the source IP address, 10000 as the source TCP port, 2.2.2.2 as the destination IP address and 80 as the destination TCP port. The output will be 1+1+1+1+10000+2+2+2+2+80 = 10092, the last digit of that is 2, so the hash output is 2. It will produce 2 every time it is fed that combination of IP addresses and ports. 

At this point it's important to note that even though PCC is most often used for spreading load across circuits, PCC itself has absolutely nothing to do with routing, routing marks or spreading load. PCC is simply a way to match packets, and not directly related to the action of then marking those matched packets even if that is its main purpose. 

Here are three lines often used for PCC, with their explanation: 

- `/ip firewall mangle add chain=prerouting action=mark-connection \ new-connection-mark=1st_conn per-connection-classifier=src-address-and-port:3/0` 

- `/ip firewall mangle add chain=prerouting action=mark-connection \ new-connection-mark=2nd_conn per-connection-classifier=src-address-and-port:3/1` 

```
/ip firewall mangle add chain=prerouting action=mark-connection \
```

```
  new-connection-mark=3rd_conn per-connection-classifier=src-address-and-port:3/2
```

Here are what the different field options mean for the purpose of packet matching, these are the fields that will be fed into the hashing algorithm (and, for the purpose of spreading load across links, decide what link a packet will be put on). Remember that a hash function will always produce the same input when it's fed the same output: 

- src-address: The source address of a client will always be the same, so all traffic from a particular client will always match the same PCC matcher, and will always be put on the same link. 

- dst-address: The destination address of a specific server will always be the same, so all traffic to that server (say, the Mikrotik Wiki) will always match the same PCC matcher, and will always be put on the same link. 

- both-addresses: The source and destination IP pair between the same client and server will always be the same, so all traffic between one specific client and a specific server (say, your laptop and the Mikrotik Wiki) will always match the same PCC matcher, and will always be put on the same link. 

- src-port: Source ports of clients are usually randomly chosen when the connection is created, so across many connections different source ports will be fed into the hash function, and different PCC matchers will match and traffic will go across different links. However, some client protocols always choose the same source port, and servers behind your router will mostly likely always use the same service port to send traffic back to their clients. A web server behind your router would send most traffic from its HTTP (80) and HTTPS (443) ports, and that traffic would always match the same PCC matcher and would be put on the same link. 

- dst-port: Destination ports of clients are usually well defined service ports, all HTTP (80) traffic between your clients and servers on the Internet would always match the same PCC matcher, and would be put on the same link. However, the same clients doing HTTPS (443) traffic could match a different PCC matcher, and would go across a different link. 

- both-ports: Since the client port is (usually) randomly chosen, the combination of the two ports is (usually) random and will spread load across links. 

- src-address-and-port: Same caveat as src-port. 

- dst-address-and-port: Same caveat as dst-port. 

both-addresses-and-ports: This is the most random way to spread traffic across links, since it has the most number of variables. 

It's important to note that even though the hash function discussed in this article is greatly simplified and not what is used in real life, it nicely demonstrates another property of hash functions: two completely different inputs can produce the same output. In our example, 3 % 3 = 0, and 6 % 3 = 0; we get back 0 when we feed it a 3 as well as when we feed it a 6. The same is true for the actual function used for PCC, even though I don't know what it is we do know from the definition that it produces a 32 bit value as output. IP addresses are 32 bit, and ports are 16 bit, so assuming that we're using both-addresses-andports, we'd be feeding it 32+32+16+16 = 96 bits of input and would only receive 32 bits back, so it must be producing the same output for different inputs. This means that two completely unrelated connections could match the same PCC matcher, and would be put on the same line. PCC works better the more connections you put across it so that the hash function has more chances to produce different outputs.
