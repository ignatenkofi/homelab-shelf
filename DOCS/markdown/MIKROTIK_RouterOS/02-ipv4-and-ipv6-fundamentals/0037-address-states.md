## Address states 

When an auto-configuration address is assigned it can be in one of the following states: 

_**`tentative`**_ - in this state host verifies that the address is unique. Verification occurs through duplicate address detection. 

- _**`preferred`**_ - at this state address is verified as unique and the node can send and receive unicast traffic to and from a preferred address. The period of time of the preferred state is included in the RA message. 

_**`deprecated`**_ - the address is still valid, but is not used for new connections. 

_**`invalid`**_ - node can no longer send or receive unicast traffic. An address enters the invalid state after the valid lifetime expires. 

The image above illustrates the relation between states and lifetimes. 

**==> picture [423 x 83] intentionally omitted <==**
