# Address Resolution Protocol (ARP)
They request for a host with a certain [[Network Layer#IP Internet Protocol|IP address]] to provide their [[Medium Access Control (MAC)|MAC address]], because the IP can get assigned to another device within the network.

It caches this knowledge for a certain time.

Only needs to know [[Medium Access Control (MAC)|MAC addresses]] from within the network.

- Broadcasts the request
- Receives a unicast as response
- Layer 2
- Stored in the **ARP table**

## ARP Spoofing/Cache Poisoning
False ARP-reply packet is used in which the attacker's MAC address is associated with the IP address of another host. With as a result that all the data sent to X reaches the attacker. *(Can be avoided by using [[Dynamic ARP Inspection (DAI)]])*