## Master-Slave Relation 

Before database synchronization can begin, a hierarchy order of exchanging information must be established, which determines which router sends Databa se Descriptor ( DD ) packets first ( Master ). The master router is elected based on the highest priority and if priority is not set then the router ID will be used. Note that it is a router priority-based relation to arranging the exchanging data between neighbors which does not affect DR/BDR election (meaning that DR does not always have to be Master ).
