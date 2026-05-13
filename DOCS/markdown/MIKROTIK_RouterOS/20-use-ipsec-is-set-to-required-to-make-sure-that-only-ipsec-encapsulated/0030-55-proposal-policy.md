## 5.5 Proposal / Policy 

- `/ip ipsec proposal add name=qkd-proposal auth-algorithms=sha256 \ enc-algorithms=aes-256-gcm pfs-group=modp2048` 

- `/ip ipsec policy add src-address=10.1.0.0/24 dst-address=10.2.0.0/24 \ peer=peer-client proposal=qkd-proposal tunnel=yes`
