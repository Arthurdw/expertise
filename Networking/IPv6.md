# IP version 6
- not used everywhere, but rising
- 16 byte *(128 bit)* address
- Build-in security features
- Bigger headers than IPv4 *(40 bytes instead of 20)*
- Uses [[Internet Control Message Protocol (ICMP)#Neighbor Discovery Protocol NDP ND|ICMP NDP]] 
## Migration from IPv4
- Dual stack *(letting a device have both an IPv4 and IPv6 address)*
- Tunnelling *(encapsulates of IPv6 in IPv4)*
- Translation *(using [[Network Address Translation (NAT)]] to translate IPv4 to IPv6)*
## Notation
- 8 groups of 4 hexadecimal digits
- Groups separated by a colon
- Written fully is called the **preferred format**
- If all zeroes, can be simplified by replacing it with a colon *(trick can only be used once, and is applied to the section that contains the most zeroes in order)* this is called the **compressed format**
### Example
- `3FFE:0088:85A0:0000:0000:8A2E:0000:7344` can be simplified to `3FFE:88:85A0::8A2E:0:7344`
- `::104E:16AE` is the same as `0000:0000:0000:0000:0000:0000:104E:16AE`
## Networking
- Same principle as the [[IPv4#Subnet mask|CIDR notation]]
- Recommended prefix is `/64` 
### Naming conventions
- Network-ID => Network Prefix
- Host ID => Interface ID
### Address types
- **Unicast**: Targets a single interface
- **Multicast**: Targets all interfaces belonging to the corresponding multicast group
- **Anycast**: Used to deliver // TODO: Continue this
- **NO Broadcast**: // TODO: Continue this
#### Important addresses
- **Global unicast address**
- **[[#Link-local address]]**: `FE80::/10`
- **Loopback address**: `::1/128`
- Unspecified address *(any address)*: `::`
- Documentation address: `2001:db8::/32`
#### Link-local address
- Each interface **must** have a link-local [[IPv6]] address
- Can only be used for **communication** with neighbors
#### Multicast address
- **All nodes**: `FF02::1`
	- Similar to [[IPv4#^e59963|IPv4 broadcast]]
- **All routers**: `FF02::2`

// TODO: Document SLAAC