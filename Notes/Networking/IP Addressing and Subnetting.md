# **IP Addressing and Subnetting**
IP addressing and subnetting are fundamental to understanding how networks communicate. Every device on a network, whether it's a computer, a smartphone, or a server, needs a unique identifier to send and receive information. This identifier is the IP address. 
Subnetting, on the other hand, allows us to divide a large network into smaller, more manageable networks, improving efficiency and security.

## **Understanding IP Addresses**
An IP address is a numerical label assigned to each device participating in a computer network that uses the Internet Protocol for communication. It serves two main functions: identifying the host or network interface and providing the location of the host in the network. There are two main versions of IP addresses: IPv4 and IPv6.

# **IPv4 Addresses**
IPv4 addresses are the most widely used, although they are gradually being replaced by IPv6. An IPv4 address is a 32-bit number, typically written in dotted decimal notation as four octets (bytes) separated by periods. Each octet represents a number between 0 and 255. An octet is 8 bits, and 8 bits actually equal 1 byte, so we also refer to an IPv4 address as having 4 bytes. This address actually contains two parts: the network portion that tells us which network it's on, and the host portion that tells us which host on that network it is.

Each network interface (network cards, network printers, or routers) is assigned a unique IP address.

### Network and Gateway Addresses
The `two` additional `IPs` added in the `IPs column` are reserved for the so-called `network address` and the `broadcast address`. Another important role plays the `default gateway`, which is the name for the IPv4 address of the `router` that couples networks and systems with different protocols and manages addresses and transmission methods. It is common for the `default gateway` to be assigned the first or last assignable IPv4 address in a subnet. 
This is not a technical requirement, but has become a de-facto standard in network environments of all sizes.

### Broadcast Address
The `broadcast` IP address's task is to connect all devices in a network with each other. `Broadcast` in a network is a message that is transmitted to all participants of a network and does not require any response. In this way, a host sends a data packet to all other participants of the network simultaneously and, in doing so, communicates its `IP address`, which the receivers can use to contact it. This is the `last IPv4` address that is used for the `broadcast`.

Example: 192.168.1.100

In this example, each number (192, 168, 1, and 100) is an octet. This address uniquely identifies a device on a network.

IPv4 addresses are divided into classes (A, B, C, D, and E) that determine the network size and the number of hosts it can accommodate.

-  Class A: 0.0.0.0 to 127.255.255.255 (Supports very large networks. e.g., large corporations). The first octet indicates the network, and the remaining three octets represent the host.
-  Class B: 128.0.0.0 to 191.255.255.255 (Supports medium-sized networks. e.g., universities). The first two octets represent the network, and the last two represent the host.
-  Class C: 192.0.0.0 to 223.255.255.255 (Supports small networks. e.g., home networks, small businesses). The first three octets represent the network, and the last octet represents the host.
-  Class D: 224.0.0.0 to 239.255.255.255 (Used for multicast addressing).
-  Class E: 240.0.0.0 to 255.255.255.255 (Reserved for experimental purposes).

Real-world Example: A large company like Google, with millions of devices, might have initially used Class A addresses. A small business with a single office might use Class C addresses.

Hypothetical Scenario: A university wants to set up its network. Knowing the number of devices, they choose Class B addresses as it fits their network size.

# IPv6 Addresses
IPv6 addresses were developed to overcome the limitations of IPv4, primarily the exhaustion of available addresses. IPv6 addresses are 128-bit addresses, usually written in hexadecimal notation, separated by colons.

Example: 2001:0db8:85a3:0000:0000:8a2e:0370:7334

This address is much larger and more complex than an IPv4 address, allowing for a vastly larger number of unique addresses. It can be simplified by omitting leading zeros in each group and replacing consecutive groups of zeros with a double colon (::), but only once in an address. So, 2001:0db8:85a3:0000:0000:8a2e:0370:7334 can be simplified to 2001:db8:85a3::8a2e:370:7334.

IPv6 is a protocol with many new features, which also has many other advantages over IPv4:
-  Larger address space
-  Address self-configuration (SLAAC)
-  Multiple IPv6 addresses per interface
-  Faster routing
-  End-to-end encryption (IPsec)
-  Data packages up to 4 GByte

IPv6 addresses also have different types:

-  Unicast: Identifies a single interface.
-  Multicast: Identifies a group of interfaces.
-  Anycast: Identifies a group of interfaces, but the packet is delivered to only one of them (the nearest one).

Real-world Example: Modern cloud providers like AWS and Azure use IPv6 addresses extensively for their services.

Hypothetical Scenario: A new data center is being built, and the system admins decide to use IPv6 to future-proof their infrastructure and avoid IPv4 address exhaustion.

## Public vs. Private IP Addresses
IP addresses can be classified into public and private addresses. This distinction is crucial for network security and routing.

## Public IP Addresses
Public IP addresses are globally unique and are assigned to organizations by Internet Service Providers (ISPs). These addresses are used for communicating over the internet. A device with a public IP address can be directly accessed from the internet.

Example: Your home router or your company's web server has a public IP address.

Real-world Example: A web server needs a public IP address to be accessible by users worldwide.

## Private IP Addresses
Private IP addresses are used within a private network, such as a home or office network. These addresses are not routable over the internet. Devices with private IP addresses use Network Address Translation (NAT) to communicate with the internet through a router that has a public IP address.

The ranges of private IP addresses are:

-  Class A: 10.0.0.0 to 10.255.255.255
-  Class B: 172.16.0.0 to 172.31.255.255
-  Class C: 192.168.0.0 to 192.168.255.255

Example: Most home networks use the 192.168.1.0/24 range. Your computer, smartphone, and other devices connected to your home Wi-Fi likely have IP addresses in this range.

Real-world Example: A company uses private IP addresses internally and then uses NAT on their router to allow employees to access the internet.

Hypothetical Scenario: A small office sets up a network using the 192.168.1.0/24 range. All computers within the office network get an IP from this range. The router then translates these private IPs to a single public IP when accessing external websites.

# Subnetting
Subnetting is the practice of dividing a network into two or more smaller networks or subnets. It allows you to improve network organization, enhance security, and optimize performance.

With the help of subnetting, we can create a specific subnet by ourselves or find out the following outline of the respective network:
-  Network address
-  Broadcast address
-  First host
-  Last host
-  Number of hosts

The bits in the host part can be changed to the first and last address. The first address is the network address, and the last address is the broadcast address for the respective subnet.

The network address is vital for the delivery of a data packet. If the network address is the same for the source and destination address, the data packet is delivered within the same subnet. If the network addresses are different, the data packet must be routed to another subnet via the default gateway.

The subnet mask determines where this separation occurs.

## Why Subnet?

-  Improved Security: Isolating sensitive resources into separate subnets can limit the impact of security breaches.
-  Reduced Network Congestion: By dividing a large network into smaller ones, you reduce the amount of traffic on each subnet.
-  Simplified Network Management: Smaller networks are easier to manage and troubleshoot.
-  Optimized Performance: Subnetting allows you to allocate network resources more efficiently.

## Subnet Mask
A further separation of these classes into small networks is done with the help of subnetting. This separation is done using the netmasks, which is as long as an IPv4 address. As with classes, it describes which bit positions within the IP address act as network part or host part.

A subnet mask is used to identify the network and host portions of an IP address. It's a 32-bit number that, when combined with an IP address, determines the network address and the host address.

Example: 255.255.255.0 or /24 in CIDR notation.

In this subnet mask, the first 24 bits are used for the network address, and the remaining 8 bits are for the host address.

## Subnetting Example
Let's say you have a Class C network 192.168.1.0 with a subnet mask of 255.255.255.0 (/24). This allows for 254 usable host addresses (2^8 - 2, subtracting the network and broadcast addresses). If you want to create two subnets, you need to borrow one bit from the host portion.

    Original Network:
        Network Address: 192.168.1.0
        Subnet Mask: 255.255.255.0 (/24)
        Usable Hosts: 254

    Subnetted Networks:
        Subnet 1: 192.168.1.0/25 (Subnet Mask: 255.255.255.128)
            Network Address: 192.168.1.0
            Usable Hosts: 126
        Subnet 2: 192.168.1.128/25 (Subnet Mask: 255.255.255.128)
            Network Address: 192.168.1.128
            Usable Hosts: 126

By borrowing one bit, we've created two subnets, each with 126 usable host addresses.

Real-world Example: A company might subnet its network to separate its sales and engineering departments.

Hypothetical Scenario: A system administrator needs to set up three separate networks for different departments: Marketing, Sales, and Support. Each department requires approximately 50 hosts. Using a /24 network would be wasteful, so the administrator decides to subnet the network into three smaller subnets using appropriate subnet masks.

# CIDR
Classless Inter-Domain Routing (CIDR) is a method of representation and replaces the fixed assignment between IPv4 address and network classes (A, B, C, D, E). The division is based on the subnet mask or the so-called CIDR suffix, which allows the bitwise division of the IPv4 address space and thus into subnets of any size. The CIDR suffix indicates how many bits from the beginning of the IPv4 address belong to the network. It is a notation that represents the subnet mask by specifying the number of 1-bits in the subnet mask.

Let us stick to the following IPv4 address and subnet mask as an example:
-  IPv4 Address: 192.168.1.0
-  Subnet mask: 255.255.255.0

Now the whole representation of the IPv4 address and the subnet mask would look like this:
-  CIDR: 192.168.1.0/24
Here, /24 indicates that the first 24 bits of the IP address (192.168.1) represent the network, and the remaining 8 bits represent the host (0).
OCTET:      1st         2nd         3rd        4th
Binary: 1111 1111 . 1111 1111 . 1111 1111 . 0000 0000 (/24)
Decimal:   255    .    255    .    255    .     0

# MAC Address
Each host in a network has its own 48-bit (6 octets) Media Access Control (MAC) address, represented in hexadecimal format. MAC is the physical address for our network interfaces.

A MAC address is a unique identifier used as a hardware address. When you want to get access to the Internet, your machine needs to have a device called a network interface card.

This network adapter has its own hardware address that's used to identify your machine. A MAC address for an Ethernet device.

MAC addresses are given to network adapters when they are manufactured. Each manufacturer has an Organizationally Unique Identifier (OUI) to identify them as the manufacturer. This OUI is denoted by the first 3 bytes of the MAC address.

This is because the MAC address addresses the physical connection (network card, Bluetooth, or WLAN adapter) of a host. Each network card has its individual MAC address, which is configured once on the manufacturer's hardware side but can always be changed, at least temporarily.

Let's have a look at an example of such a MAC address:
-  DE:AD:BE:EF:13:37
-  DE-AD-BE-EF-13-37
-  DEAD.BEEF.1337

When an IP packet is delivered, it must be addressed on layer 2 to the destination host's physical address or to the router / NAT, which is responsible for routing. Each packet has a sender address and a destination address.

If a host with the IP target address is located in the same subnet, the delivery is made directly to the target computer's physical address. However, if this host belongs to a different subnet, the Ethernet frame is addressed to the MAC address of the responsible router (default gateway). If the Ethernet frame's destination address matches its own layer 2 address, the router will forward the frame to the higher layers. Address Resolution Protocol (ARP) is used in IPv4 to determine the MAC addresses associated with the IP addresses.

## Loopback
The loopback is a special network interface that refers to your own computer.

It allows your computer to send and receive network traffic to itself.

The most common loopback IP address is: 127.0.0.1

Think of it as your computer talking to itself — like testing a microphone by speaking and hearing your own voice.

## Localhost
localhost is the hostname (name) that maps to the loopback IP address.

It is usually: localhost → 127.0.0.1

It's defined in your system’s hosts file (like /etc/hosts on Linux/Mac).

When you type ping localhost, your computer is really pinging itself at 127.0.0.1.

## Loopback vs. Localhost
127.0.0.1 is the loopback IP address, and localhost is the name that points to it.

They both mean "this computer", and are often used for testing servers or services locally without using an actual network.

## Default Gateway
Access point between local network and the internet.
In local network, it is a router. It is the "exit" from local network, usually routers address(e.g. 192.168.0.1). All traffic destined for the Internet goes through here. Then routes to the appropiate external network.

## Related Protocols (NAT, ARP, DHCP, DNS)

## NAT
NAT makes a device like our router act as an intermediary between the internet and a private network. So only a single, unique IP address is required to represent an entire group of computers. Translate Private IP -> Public IP and vice versa.

## ARP
Used in the same network for translating IP Address to MAC Address. Devices use ARP to acquire the MAC Address for a device. By sending out a broadcast message out on the network asking every devices, and the devices with the IP that match with the broadcast message sends back the MAC Address.

## DHCP
Automatically assigns IP Address, subnet masks, DNS server, Gateway to clients, ensuring uniqe adresses for each devices. The router normally acts as a DHCP Server.

## DNS
The Domain Name System (DNS) is essentially the internet's phonebook. Its primary function is to translate human-friendly domain names (like www.example.com) into computer-friendly Internet Protocol (IP) addresses (like 192.0.2.1), which are required for devices to locate and communicate with each other on the network. Without DNS, you'd have to memorize complex numerical IP addresses to visit websites.

## DNS Resolution
DNS Resolution is the multi-step process that a computer follows to find a domain's IP address. This typically involves several types of DNS servers working together:

1.    Query Initiation: When you enter a domain name into your browser, your computer first checks its local cache. If the IP address isn't found, it sends a query to a DNS Recursor (or Resolver), typically operated by your Internet Service Provider (ISP).
2.    Root Name Server Query: If the Recursor doesn't have the IP cached, it contacts one of the Root Name Servers (the top of the DNS hierarchy). The Root server responds by directing the Recursor to the correct Top-Level Domain (TLD) Name Server (e.g., for .com, .org).
3.    TLD Name Server Query: The Recursor contacts the TLD server, which in turn directs it to the Authoritative Name Server for that specific domain.
4.    Authoritative Name Server Query: The Authoritative Name Server is the one that holds the definitive DNS records (including the IP address) for the domain. It sends the IP address back to the Recursor.
5.    Response and Connection: The Recursor sends the IP address back to your browser, which then uses it to connect directly to the website's server and load the page. The Recursor also caches the IP address for a set period to speed up future requests for that same domain.
