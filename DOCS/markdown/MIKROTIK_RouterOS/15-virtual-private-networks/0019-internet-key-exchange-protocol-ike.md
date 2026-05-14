## Internet Key Exchange Protocol (IKE) 

The Internet Key Exchange (IKE) is a protocol that provides authenticated keying material for the Internet Security Association and Key Management Protocol (ISAKMP) framework. There are other key exchange schemes that work with ISAKMP, but IKE is the most widely used one. Together they provide means for authentication of hosts and automatic management of security associations (SA). 

Most of the time IKE daemon is doing nothing. There are two possible situations when it is activated: 

There is some traffic caught by a policy rule which needs to become encrypted or authenticated, but the policy doesn't have any SAs. The policy notifies the IKE daemon about that, and the IKE daemon initiates a connection to a remote host. IKE daemon responds to remote connection. In both cases, peers establish a connection and execute 2 phases: 

Phase 1 - The peers agree upon algorithms they will use in the following IKE messages and authenticate. The keying material used to derive keys for all SAs and to protect following ISAKMP exchanges between hosts is generated also. This phase should match the following settings: 

authentication method 

DH group encryption algorithm exchange mode hash algorithm NAT-T DPD and lifetime (optional) 

Phase 2 - The peers establish one or more SAs that will be used by IPsec to encrypt data. All SAs established by the IKE daemon will have lifetime values (either limiting time, after which SA will become invalid, or the amount of data that can be encrypted by this SA, or both). This phase should match the following settings: 

IPsec protocol 

mode (tunnel or transport) authentication method PFS (DH) group lifetime 

**==> picture [13 x 13] intentionally omitted <==**

There are two lifetime values - soft and hard. When SA reaches its soft lifetime threshold, the IKE daemon receives a notice and starts another phase 2 exchange to replace this SA with a fresh one. If SA reaches a hard lifetime, it is discarded. 

**==> picture [13 x 13] intentionally omitted <==**

Phase 1 is not re-keyed if DPD is disabled when the lifetime expires, only phase 2 is re-keyed. To force phase 1 re-key, enable DPD. 

1189 

**==> picture [13 x 13] intentionally omitted <==**

PSK authentication was known to be vulnerable against Offline attacks in "aggressive" mode, however recent discoveries indicate that offline attack is possible also in the case of "main" and "ike2" exchange modes. A general recommendation is to avoid using the PSK authentication method. 

IKE can optionally provide a Perfect Forward Secrecy (PFS), which is a property of key exchanges, that, in turn, means for IKE that compromising the long term phase 1 key will not allow to easily gain access to all IPsec data that is protected by SAs established through this phase 1. It means an additional keying material is generated for each phase 2. 

The generation of keying material is computationally very expensive. Exempli Gratia, the use of the modp8192 group can take several seconds even on a very fast computer. It usually takes place once per phase 1 exchange, which happens only once between any host pair and then is kept for a long time. PFS adds this expensive operation also to each phase 2 exchange.
