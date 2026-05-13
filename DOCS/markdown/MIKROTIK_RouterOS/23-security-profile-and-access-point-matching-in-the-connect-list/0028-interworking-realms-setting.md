## Interworking Realms setting 

For more information about interworking-profiles see the manual. 

realms-raw - list of strings with hex values. Each string specifies contents of "NAI Realm Tuple", excluding "NAI Realm Data Field Length" field. 

Each hex encoded string must consist of the following fields: 

- `NAI Realm Encoding (1 byte)` 

- `NAI Realm Length (1 byte)` 

- `NAI Realm (variable)` 

- `EAP Method Count (1 byte)` 

- `EAP Method Tuples (variable)` 

For example, value "00045465737401020d00" decodes as: 

- `NAI Realm Encoding: 0 (rfc4282) - NAI Realm Length: 4 - NAI Realm: Test - EAP Method Count: 1 - EAP Method Length: 2 - EAP Method Tuple: TLS, no EAP method parameters` 

Note, that setting "realms-raw=00045465737401020d00" produces the same advertisement contents as setting "realms=Test:eap-tls". 

Refer to 802.11-2016, section 9.4.5.10 for full NAI Realm encoding. 

1426
