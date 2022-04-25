# Transport Layer
The transport layer is the third layer in the [[OSI Model]]. It allows application running on source and destination hosts to communicate with eachother. The data that has to be transmitted is split in segments. And is reassembled at the receiving host.

Because of segmentation, multiple applications can exchange data simultaniously *(multiplexing)*

It allows multiple applications to listen/send data on one host through the usage of port numbers.
## Protocols
- [[Transmission Control Protocol (TCP)]]
- [[User Datagram Protocol (UDP)]]
## Port number
The source port is first in the frame, followed by the destination port.
### Categories
- **Well known ports**: 0-1023
- **Registered ports**: 1024-49151
- **Dynamic or private ports**: 49152-65535
### Well known ports
Port | Protocol    | TCP/UDP
:-:  | :-          | :-
20   | FTP-Data    | TCP
21   | FTP-Control | TCP
22   | SSH         | TCP
23   | Telnet      | TCP
25   | SMTP        | TCP
53   | DNS         | UDP *(or TCP)*
80   | HTTP        | TCP
110  | POP3        | TCP
143  | IMAP        | TCP
161  | SNMP        | UDP
443  | HTTPS       | TCP
520  | RIP         | UDP
## Connections
The **combintion of an [[Network Layer#IP Internet Protocol|IP]] and a [[#Port number|port number]]** identifies an application on a host. We call this a **socket**. *(eg, 192.168.1.110:8080)*
### Transport connection/conversation
- Client IP + Client Port + Server IP + Server Port + Protocol
  *(192.168.1.110:50100, 192.168.50.50:80, TCP)*
