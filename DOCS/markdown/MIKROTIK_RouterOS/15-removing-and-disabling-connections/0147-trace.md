## TRACE 

This method invokes a remote, application-layer loop-back of the request message. The final recipient of the request should reflect the message received back to the client as the entity-body of a 200 (OK) response. The final recipient is either the origin server or the first proxy or gateway to receive a MaxForwards value of 0 in the request. A TRACE request must not include an entity. 

Responses to this method MUST NOT be cached. 

940
