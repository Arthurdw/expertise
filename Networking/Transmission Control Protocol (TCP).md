# Transmission Control Protocol (TCP)
- Connection oriented, as a connection *(session)* is established between the sender and the receiver
- Statefull
- Flow control *(receiver can slow down a transmitter which is too fast)*
- Reliable *(Makes sure that the transmitted segments arrive properly)*
## Initialisation
Because TCP is conenction oriented, both hosts must first set up the connection before they can send data.

- Initialisation of the [[Ethernet Switch#Duplex|full-duplex]] connection is done in 3 phases
	- Each phase uses **Control Bits *(TCP flags)*** in the header
	- The main control bits are **ACK *(Acknowledge)***, **SYN *(Synchronize)*** and **FIN *(Finished)*** ^ec0325
- Trace numbers are used throughout the connection
	- **SEQNR *(Sequence number)***: The amount of bytes that have been sent
	- **ACKNR *(Acknowledge number)***: The amount of bytes that have been received
### 3-way handshake
1. The **client** asks the server to connect for a *client-server session*
   - Control flags:
	   - SYN = 1
	   - ACK = 0
   - Track & trace:
	   - SEQNR = random **ISN *(initial sequence number)* of client**
	   - ACKNR = 0
2. The **server** confirms the *client-to-server session* and requests a *server-to-client* connection
  - Control flags:
	   - SYN = 1
	   - ACK = 1
   - Track & trace:
	   - SEQNR = random **ISN of server**
	   - ACKNR = **ISN(client) + 1**
3. The **client** confirms the *server-to-client session*
  - Control flags:
	   - SYN = 0
	   - ACK = 1
   - Track & trace:
	   - SEQNR = **ISN(client) + 1**
	   - ACKNR = **SEQNR(server step 2) + 1**

After this handshake all segments their ACK bit is set to 1.
![[3way handshake.png]] ^729239
#### Reliability
Used to put segments in the correct order at the receiver by reordering if necessary. And can be used to confirm all data has arrived, and if it hasn't retransmit a segment if necessary.
- **Sequence Number *(SEQNR)***: 
	- Byte stream number of the first data byte in its TCP segment
- **Acknowledgement Number *(ACKNR)***: 
	- Byte stream number of the **next** data byte it **expects to receive** from the other host
	- The next sequence number that the sender is expecting
	- **expectional acknowledgment**
- **Selective ACK's *(SACK)***:
	- Only the lost segments have to be re-transmitted. This is different from the default behavior, which requires all segments that were sent since the lost segement to be retransmitted.
## Windowing
Indicates how many bytes can be sent before expecting an acknowledgment. This is included in the header of every TCP segment, which allows the destination to modify the window size at any time.

This **allows flow control**. *(if the receiver their buffer is getting full)*
## 4-way handshake
Properly ends a TCP connection, requires 2 steps to end each connection. *(client-to-server and server-to-client)*

Uses the special **[[#^ec0325|FIN]]** flag, and **requires a [[#^729239|ACK]]  to confirm the termination**.
![[4-way handshake.png]]