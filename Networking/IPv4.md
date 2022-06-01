# IP version 4
- Most common today
- 4 byte *(32 bit)* address *(only 4 billion addresses -> scarcity, resolved by [[Network Address Translation (NAT)|NAT]])*
## Format
![[IPv4 format.png]]
## Subnet mask
Network ID and host ID get delimited by the Subnet Mask. If the IP is beyond the subnet mask, the packet will be sent to the default gateway.
### Types
Class | Subnet mask   | CIDR | Hosts
:-:   | :-:           | :-:  | :-
A     | 255.0.0.0     | 8    | 16 777 216
B     | 255.255.0.0   | 16   | 65 536
C     | 255.255.255.0 | 24   | 256
## Special addresses
### IP
Name              | Address                                 | Description
:-:               | :-:                                     | :-
Network address   | 0000 0000.0000 0000.0000 0000.0000 0000 | Sets all bytes to 0.
Broadcast address | 1111 1111.1111 1111.1111 1111.1111 1111 | Sets all bytes to 1.

^e59963

### Subnet 
Name                         | Address     | CIDR
:-:                          | :-:         | :-
Loopback address             | 127.0.0.0   | 8
Link-local address *(APIPA)* | 169.254.0.0 | 16
Muticast address             | 224.0.0.0   | 4

^8d0375




