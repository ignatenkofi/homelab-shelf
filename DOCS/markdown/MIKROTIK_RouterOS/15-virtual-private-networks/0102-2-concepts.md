## 2. Concepts 

PPK (Post-Quantum Pre-shared Key): An additional secret shared during IKE negotiation to resist quantum attacks. QKD: Quantum-based key distribution providing fresh symmetric keys via a Key Management Entity (KME). 

IKE SA vs ESP SA: 

IKE SA: Controls tunnel negotiation. ESP SA: Carries encrypted user data. 

Static vs Dynamic keys: 

Dynamic: ephemeral PSK or QKD-distributed secrets, used once and discarded. Static: manually set per peer, persistent across sessions.
