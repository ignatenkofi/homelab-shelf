## Encapsulating Security Payload (ESP) 

Encapsulating Security Payload (ESP) uses shared key encryption to provide data privacy. ESP also supports its own authentication scheme like that used in AH. 

ESP packages its fields in a very different way than AH. Instead of having just a header, it divides its fields into three components: 

ESP Header - Comes before the encrypted data and its placement depends on whether ESP is used in transport mode or tunnel mode. ESP Trailer - This section is placed after the encrypted data. It contains padding that is used to align the encrypted data. ESP Authentication Data - This field contains an Integrity Check Value (ICV), computed in a manner similar to how the AH protocol works, for when ESP's optional authentication feature is used.
