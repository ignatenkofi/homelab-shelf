## 1. Introduction 

This manual describes the Post-Quantum Pre-shared Key (PPK) feature in RouterOS IPsec and its integration with Quantum Key Distribution (QKD). 

PPK provides forward security against quantum attacks by using keys that are either dynamically distributed or statically configured. All PPK types (static, PSK, QKD) benefit from RFC 8784 recommendations: keys should have at least 256 bits of entropy to provide ~128 bits of post-quantum security. RouterOS supports three PPK sources: 

Static PPK — manually configured per-peer secret. PSK (Pre-shared Key) — one-time generated keys, optionally usable only for initial IKE SA. QKD — dynamically distributed keys from a QKD server. 

Dynamic keys (PSK/QKD) are consumed and invalidated after use. Static keys remain valid across sessions but offer weaker security if reused. 

**==> picture [282 x 189] intentionally omitted <==**
