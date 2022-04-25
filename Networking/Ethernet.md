# Ethernet
Ethernet runs on the [[Physical Layer]], it is a protocol which is commonly used for wired network communication. 

The physical topology of an network is a star network. This means that the devices are connected to an [[Ethernet Switch]] or [[Network Hub]].

## Standards
- [[Institute of Electrical and Electronics Engineerds (IEEE)|IEEE]] 802.3 & 802.2 Ethernet

### 802.2
Top part layer of the data link layer *([[Logical Link Control (LLC)]])*

### 802.3
Physical layer and lower part layer of the [[Data-link Layer]]. ([[Medium Access Control (MAC)]])

## Cable notation
![[Ethernet cable notation.png]]
*Image from HOWEST CS course (Computer Networks), lectured by Daan Pareit*

## Frame format
### Ethernet II frame
![[Ethernet II frame.png]]
*Image from HOWEST CS course (Computer Networks), lectured by Daan Pareit*

The **destination address** comes **first** so that your [[Network Interface Card (NIC)]] can drop frames where the Destination address does't match its own [[Medium Access Control (MAC)]] address. *(Unless promiscuous mode is enabled, this allows you to snif the network, eg in [[Wireshark]])*

The destination and source address change for every hop, as this is is only for inner network targetting and not for the packet destination/source.

Section             | Description
:-:                 | :-
Preamble            | A fixed pattern on which the [[Network Interface Card (NIC)]] listens so that it knows when a new frame starts. It removes these 8 bytes from the packet before passing it through.
Destination address | The [[Medium Access Control (MAC)]] address of the frame target.
Source address      | The [[Medium Access Control (MAC)]] address of frame source. *(where it originates from)*
Type                | 2 bytes that indicate what protocol is embedded in the data part of the frame.
Data                | The data it has to carry. *(Which are the headers & content of the layers above it)* But this **must be atleast 46 bytes** otherwise it will be regared as invalid and will be droppped. Filling bytes to achieve this amount are called **padding**. The **Maximum Transferable Unit (MTU)** is the maximum amount of bytes, which is set to 1500bytes but can be increased by using [[Jumbo Frames]].
FCS                 | The Frame Check Sequence is used to detect errors *(eg, through CRC, and a control number)*. This gets dropped by your [[Network Interface Card (NIC)]]
