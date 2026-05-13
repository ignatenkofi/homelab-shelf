## 5.4 Profiles and Peers 

- `/ip ipsec profile add name=qkd-profile ppk=qkd` 

- `/ip ipsec peer add address=10.20.1.2 exchange-mode=ike2 \ name=peer-client profile=qkd-profile proposal-check=obey` 

- `/ip ipsec identity add peer=peer-client profile=qkd-profile` 

PPK options for profiles: 

**==> picture [291 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
Option Description<br>no PPK disabled.<br>psk One-time PSK used for IKE and ESP rekey.<br>psk-ike-initial PSK used only for the initial IKE SA (renamed from  psk-ike-only ).<br>qkd Keys retrieved from QKD server.<br>**----- End of picture text -----**<br>
