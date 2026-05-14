## Secrets 

RoMON protocol secrets are used for message authentication, integrity check and replay prevention by means of hashing message contents with MD5. 

For each interface, if the interface-specific secret list is empty, a global secret list is used. When sending out, messages are hashed with the first secret in list if list is not empty and first is not "empty secret" (empty string = ""), otherwise, messages are sent unhashed. When received, unhashed messages are only accepted if a secret list is empty or contains "empty secret", hashed messages are accepted if they are hashed with any of the secrets in list. 

This design allows for the incremental introduction and/or change of secrets in-network without RoMON service interruption and can happen over RoMON itself, e.g.: 

initially, all routers are without secrets; 

- configure each router one by one with secrets="","mysecret" - this will make all routers still send unprotected frames, but they all will be ready to accept frames protected with secret "mysecret"; 

- configure each router one by one with secrets="mysecret","" - this will make all routers use secret "mysecret", but also still accept unprotected frames (from routers that have not yet been changed); 

- configure each router with secrets="mysecret" - this will make all routers use secret "mysecret" and also only accept frames protected with "mysecret"; 

Changing of secret in a network should be performed in a similar fashion where for some time both secrets are in use in network.
