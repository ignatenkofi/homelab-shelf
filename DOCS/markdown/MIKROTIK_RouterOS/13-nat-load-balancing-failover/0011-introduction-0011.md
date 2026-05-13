## Introduction 

In this article, we will look at another advanced method of failover using recursive routing and scopes from the routing section. Recursive routing occurs when a route (either static or dynamically learned) has a next-hop that is not directly connected to the local router. It is necessary to restrict a set of routes that can be used to look up immediate next-hops. Nexthop values of RIP or OSPF routes, for example, are supposed to be directly reachable and should be looked up only using connected routes. This is achieved using a scope and target-scope properties.
