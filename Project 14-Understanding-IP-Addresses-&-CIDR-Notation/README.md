# Understanding IP Addresses and CIDR Notation

## Introduction to IP Addresses

An IP Address is a unique address that identifies a device on the internet or a local network. IP stands for `Internet Protocal` which is the set of rules governing the format of data sent via the internet or local network. In essence, IP addresses are the identifier that allows information to be sent between devices on a network: they contain locataion information and make devices accessible for communication. The internet needs a way to differentiate between different computers, routers, and websites. IP addresses provide a way of doing so and form an essential part of how the internet works.


##### What is an IP Address?


An IP address is a string of numbers seperated by periods. IP addresses are expressed as a set of four numbers -- an example address might be 88.99.987.9. Each number in the set ca range from 0 to 255. So, the full IP addressing range goes from 0.0.0.0 to 255.255.255.255. IP addresses are not random. They are mathematically produced and allocated by the Internet Assigned Numbers Authority (IANA), a devision of the Internet Corporation for Assigned Names and Numbers (ICANN). ICANN is a non-profit organisation that was established in the United States in 1998 to help maintain the security of the internet and allow it to be usable by all. Each time anyone registers a domain on the internet, they go through a domain name registrar, who pays a small fee to ICANN to register the domain.


![ip octet](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/3fa9166d-4cae-457d-9760-2bc92e659ef6)


## SUBNETTING AND SUBNET MASKS

Subnetting is the practice of dividing a network into two or smaller networks. It increases routing efficiency, which helps to enhance the security of the network and reduces the size of the broadcast domain.

IP subnetting designates high-order bits from the host as part of the network prefix. This method divides a network into smaller subnets.

It also helps you to reduce the size of the routing tables, which is stored in routers. This method also helps you to extend the existing IP address base and restructure the IP address.


![subnet and mask](https://github.com/AndromedaIsComingg/DevOps-Projects-Darey.io/assets/140917780/026c7669-067a-4120-9321-ea4ab8cdeff7)


A `Subnet Mask` is a 32 bits address used to distinguish between a network address and a host address in IP address. A subnet masks identifies which part of an IP address is the network address and the host address. They are not shown inside the data packets traversing the internet. They carry the destination IP address, which a router will match with a subnet


##### CIDR Notation and Address Aggregation

Classless Inter-Domain Routing (CIDR) is an IP address allocation method that improves data routing efficiency on the internet. Every machine, server, and end-user device that connects to the internet has a unique number, called an IP address, associated with it. Devices find and communicate with each other by using these IP addresses. Organisations use CIDR to allocate IP addreses flexibly and efficiently in their networks. It represent blocks of IP addresses, to get the number of addresses a CIDR block represent, you calculate 2^(32-prefix), where prefix is the number after the slash. For instance /16 contains 2^(32-16) = 2^16 = 65,536 






