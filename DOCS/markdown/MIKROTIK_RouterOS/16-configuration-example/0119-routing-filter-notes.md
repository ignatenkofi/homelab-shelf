## Routing Filter Notes 

On BGP output routing filters are executed before BGP itself is modifying attributes, for example, if `nexthop-choice` is set to `force-self` , then the gateway set in the routing filters will be overridden. 

On BGP input routing filters are applied to the received attributes, which means that, for example, setting the gateway will work no matter what `nexhopchoice` value is set.
