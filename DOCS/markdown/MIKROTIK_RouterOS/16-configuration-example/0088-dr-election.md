## DR Election 

1000 

DR and BDR routers are elected from data received in the Hello packet. The first OSPF router on a subnet is always elected as Designated Router, when a second router is added it becomes Backup Designated Router. When an existing DR or BDR fails new DR or BDR is elected to take into account configured router priority. The router with the highest priority becomes the new DR or BDR. 

Being Designated Router or Backup Designated Router consumes additional resources. If Router Priority is set to 0, then the router is not participating in the election process. This is very useful if certain slower routers are not capable of being DR or BDR.
