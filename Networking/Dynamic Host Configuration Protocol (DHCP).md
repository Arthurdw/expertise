# Dynamic Host Configuration Protocol (DHCP)
Assigns IP addresses dynamically to hosts within its assigned network. Mainly used for [[IPv4]], can also be used for [[IPv6]], but v6 can also use [[IPv6#^ce870f|SLAAC]].

This is a [[Application Layer]] protocol, and this utilizes [[User Datagram Protocol (UDP)]] *(port 67 and 68)*.

Range is set in pools. *(which alows eg for /16 [[IPv4#Subnet|bit CIDR]] to be further subnetted into a /24)*

If the DHCP server does not assign an IP for the host, will choose an [[IPv4#^8d0375|Link-local address]].
## Properties
- Subnet mask
- Lease time *(ttime the IP is valid)*
- IP address of the default gateway
- IP address of the DNS server
## DORA (IPv4)
- Sends discover to **255.255.255.255**
- DHCPOFFER allows multiple DHCP servers to run in a single network and let the DHCP client choose.
![[DHCP DORA.png]]
## SARR (IPv6)
- **S**OLICT
- **A**DVERTISE
- **R**EQEUST
- **R**EPLY

### Differences with DORA
- **NO** default gateway
- Uses [[IPv6]] multicasting to **FF02::1:2** *(instead of the [[IPv4]] broadcast)*
- Uses [[User Datagram Protocol (UDP)]] port 546 & 547