# Medium Access Control (MAC)
- 6 byte *(48 bits)*
- Globally unique
- Typically represented in hexadecimal form
- Also referred to as the **Burned-in-address (BIA)**
- Can be generated/spoofed with software

## Notations
Notation | notation
:-       | :-
Linux    | XX:XX:XX:XX:XX:XX
Windows  | XX-XX-XX-XX-XX-XX
Cisco    | XXXX.XXXX.XXXX

## Special addresses
- Broadcast sets all bits to 1, so the address is **FF:FF:FF:FF:FF:FF**.
- Multicast starts with 01:00:5E

## Orginazitionally Unique Identifier (OUI)
The **first 3 bytes** are static for a vendor, they have been assigned this by the [[Institute of Electrical and Electronics Engineerds (IEEE)]]. The other 3 bytes are chosen by the vendor.
