# Internet Control Message Protocol (ICMP)
This is a protocol which is used to send error messages. This is usefull because [[Network Layer#IP Internet Protocol|IP]] is best effort, so ICMP can give us feedback on issues related to [[Network Layer#IP Internet Protocol|IP]] packets. 

- Layer 3 protocol
## Example messages
- Host confirmation *([[Physical Layer Terms#Round trip time RTT|ping]])*
- Destination or host unreachable
- Time exeeded *(if TTL is 0)*
## Neighbor Discovery Protocol (NDP/ND)
- Sends a **neighbor solicitation** *(multicast)* instead of an [[Address Resolution Protocol (ARP)|ARP]] broadcast
- Receives a **neighbor advertisement** *(unicast)* as response
- Because it uses ICMP its a layer 3 protocol
- Stored in the **Neighbor Discovery table**
### Advantages compared to ARP
- Multicast allows the NIC to determine if the neighbor solicitation is for itself without having to let the OS proccess it
### Disadvantages
- Frames are larger -> more overhead