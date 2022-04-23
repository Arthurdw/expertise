# Ethernet Switch
Forwards all frames to the port with the destination device on it. *(except for multicast/broadcast)* It learns this via the [[Medium Access Control (MAC)]] address, therefore a switch is called a Layer 2 Switch *([[OSI Model]])*.

The dataset of the [[Medium Access Control (MAC)]] addresses is called a **MAC address table**. In this table, addresses are associated with a pysical port on the switch. Records are only kept for a limited time. *(typically 5 minutes)*

If it doesn't know where to send it, it sends it to everyone.

## Duplex
Unlike a  [[Network Hub]], switches run in full duplex. This means that every connection can receive and transmit data without having to wait for other hosts to clear the line. *(As the switch buffers this internally)*