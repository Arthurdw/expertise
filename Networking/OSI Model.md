# OSI Model
A component based way to represent the communication between hosts.

id   | name                   | description
:--- | :---:                  | :---
7    | [[Application Layer]]  | The top protocol which is specific to the application. *(eg HTTP, FTP, ...)*
6    | [[Presentation Layer]] | Encoding/decoding of data.
5    | [[Session Layer]]      | Sessions get managed here. *(eg for Voice over IP)*
4    | [[Transport Layer]]    | Get segment to the right process. *(via ports)*
3    | [[Network Layer]]      | Get packets to the right host. *(via IP)*
2    | [[Data-link Layer]]    | Get frames to the right network. (via MAC)
1    | [[Physical Layer]]     | How the bits are sent. *(eg cable)*