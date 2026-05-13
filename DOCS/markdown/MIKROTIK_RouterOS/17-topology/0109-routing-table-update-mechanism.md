## Routing Table Update Mechanism 

Illustration below tries to explain in more user friendly form on how routing table update mechanism is working. 

1082 

**==> picture [504 x 213] intentionally omitted <==**

Routing protocols continuously loop through following procedures: 

- " main " process waits for updates from other sub tasks (1); 

- " main " starts to calculate new routes (2..4) if: 

   - update from sub task is received; 

   - protocol has not published all routes; 

configuration has changed or link state has changed. 

during new route calculation (5) following event occur: 

all received updates are applied to the route; gateway reachability is being determined; recursive route is being resolved; 

- " publish " event is called where " current " routes are being published. During this phase, " current " routes will not change, but protocols can still 

receive and send updates (6). 

Do cleanup and free unused memory (7). In this step everything that is no longer used in new " current " table is removed (routes, attributes, etc.). 

Consider " updated " and " current " as two copies of routing table, where " current " table (2) is the one used at the moment and " updated " (1) is table of candidate routes to be published in the next publish event (3 and 4). This method prevents protocols to fill memory with buffered updates while " main " process is doing " publish ", instead protocols sends the newest update directly to "main" process which then copies new update in " updated " table. A bit more complicated is OSPF, it internally has similar process to select current OSPF routes which then are sent to the  " main " for further processing. 

1083
