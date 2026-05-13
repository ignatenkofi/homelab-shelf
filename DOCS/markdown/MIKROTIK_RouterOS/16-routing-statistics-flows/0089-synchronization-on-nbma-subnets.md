## Synchronization on NBMA Subnets 

Database synchronization on NBMA networks is similar to that on broadcast networks. DR and BDR are elected, databases initially are exchanged only with DR and BDR routers and flooding always goes through the DR. The only difference is that Link State Updates must be replicated and sent to each adjacent router separately.
