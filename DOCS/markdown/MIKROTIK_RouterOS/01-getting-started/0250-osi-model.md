## OSI Model 

The Open Systems Interconnection (OSI) model is a 7-layer model that today is used as a teaching tool. The OSI model was originally conceived as a standard architecture for building network systems, but in real-world networks are much less defined than the OSI model suggests. 

- Layer 7 (Application) - a protocol that defines the communication between the server and the client, for example, HTTP protocol. If the web browser wants to download an image, the protocol will organize and execute the request; 

- Layer 6 (Presentation) - ensures data is received in a usable format. Encryption is done here (but in reality it may not be true, for example, IPSec); 

- Layer 5 (Session) - responsible for setting up, managing and closing sessions between client and server; 

- Layer 4 (Transport) - transport layers primary responsibility is assembly and reassembly, a data stream is divided into chunks (segments), assigned sequence numbers and encapsulated into protocol header (TCP, UDP, etc.); 

- Layer 3 (Network) - responsible for logical device addressing, data is encapsulated within an IP header and now called "packet"; Layer 2 (Data link) - Data is encapsulated within a custom header, either 802.3 (Ethernet) or 802.11 (wireless) and is called "frame", handles flow control; 

- Layer 1 (Physical) - Communication media that sends and receives bits, electric signaling, and hardware interface;
