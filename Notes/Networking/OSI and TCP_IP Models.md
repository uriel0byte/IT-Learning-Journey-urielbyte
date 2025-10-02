# Introduction to Networking Concepts: TCP/IP, OSI Model
The TCP/IP model uses the TCP/IP protocol suite, refer to as TCP/IP. These protocols work together to specify how data should be gathered, addressed, transmitted, and routed through a network. Using the TCP/IP model, we can see how these protocols are used to show the breakdown of how a packet travels through the network.

## The Importance of Networking
-  Server Configuration: Configuring network interfaces, assigning IP addresses, and setting up routing.
-  Troubleshooting: Diagnosing network connectivity issues, identifying bottlenecks, and resolving performance problems.
-  Security: Implementing network security measures, such as firewalls, intrusion detection systems, and VPNs.
-  Automation: Using scripting (like your existing Bash skills) to automate network configuration and monitoring tasks.
-  Cloud Computing: Managing virtual networks and connecting on-premises systems to cloud resources.

---

# The OSI Model: A Conceptual Framework
The Open Systems Interconnection (OSI) model is a conceptual framework that standardizes the functions of a telecommunication or computing system into seven abstraction layers. It's a theoretical model, but it provides a valuable way to understand how network communication works.

### The seven layers of the OSI model are:

1.  Physical Layer: Deals with the physical cables, radio frequencies, and other hardware used to transmit data. It defines aspects such as voltage levels, data rates, and physical connectors. Example: Ethernet cables, fiber optic cables, wireless signals.
2.  Data Link Layer: Provides error-free transmission of data frames between two directly connected nodes. It handles physical addressing (MAC addresses) and framing of data. Example: Ethernet protocol, MAC address.
3.  Network Layer: Handles routing of data packets from source to destination across multiple networks. It uses logical addressing (IP addresses) to identify devices. Example: IP protocol, routers.
4.  Transport Layer: Provides reliable and ordered delivery of data between applications. It handles segmentation, error recovery, and flow control. Example: TCP and UDP protocols.
5.  Session Layer: Manages connections between applications, establishing, coordinating, and terminating conversations, dialogues, and sessions between applications. Example: managing login sessions, establishing a connection to a database server.
6.  Presentation Layer: Deals with data representation, encryption, and decryption. It ensures that data is in a format that can be understood by both communicating applications. Example: SSL/TLS encryption, data compression.
7.  Application Layer: Provides network services to applications, such as email, web browsing, and file transfer. Example: HTTP, SMTP, FTP protocols.

### Deep Dive into Each Layer

1.  Physical Layer: Imagine plugging an Ethernet cable into your computer. The physical layer defines the specifications for that cable, the connector (RJ45), and the electrical signals that travel through it. Different cabling standards (e.g., Cat5e, Cat6) operate at different speeds, all governed by the physical layer.
2.  Data Link Layer: Each network interface card (NIC) has a unique Media Access Control (MAC) address. When your computer sends data to another device on the same local network, it uses the destination's MAC address. The data link layer ensures that the data frame arrives correctly at the intended recipient on that local network. This layer includes protocols such as Ethernet and ARP (Address Resolution Protocol).
3.  Network Layer: When your computer needs to send data to a device on a different network (e.g., a server on the internet), the network layer comes into play. It uses IP addresses to route packets across multiple networks. Routers examine the destination IP address of each packet and forward it to the next hop along the path to its destination.
4.  Transport Layer: The Transport Layer is crucial for reliable communication. TCP, a protocol within this layer, establishes a connection, ensures that data is delivered in the correct order, and retransmits lost packets. UDP, another protocol, offers faster but less reliable communication as it doesn't guarantee delivery or order. Streaming video often uses UDP because some dropped packets are tolerable, but speed is essential.
5.  Session Layer: Consider a scenario where you're logged into a website. The session layer manages that connection. It authenticates you, keeps track of your session, and terminates the connection when you log out or after a period of inactivity.
6.  Presentation Layer: When you visit a secure website (HTTPS), the presentation layer handles the SSL/TLS encryption. It ensures that the data transmitted between your browser and the server is encrypted, protecting it from eavesdropping. It also handles data formatting, such as converting data between different character sets.
7.  Application Layer: This is the layer that users interact with directly. When you send an email using an email client, the application layer protocol (SMTP) is used to send the email to a mail server. When you browse the web, the HTTP protocol is used to retrieve web pages from a web server.

### Hypothetical Scenario

Imagine you're accessing a website (e.g., example.com) from your computer. Here's how the OSI model comes into play:
1.  Application Layer: Your web browser (e.g., Chrome, Firefox) initiates an HTTP request to example.com.
2.  Presentation Layer: The browser encrypts the data using TLS/SSL if the website uses HTTPS.
3.  Session Layer: A session is established between your browser and the web server.
4.  Transport Layer: TCP ensures reliable delivery of the HTTP request to the web server.
5.  Network Layer: IP routes the packets across the internet to the server's IP address.
6.  Data Link Layer: Ethernet frames the packets for transmission over the local network.
7.  Physical Layer: Electrical signals transmit the data over the Ethernet cable.

The web server then processes the request and sends a response back to your computer, following the same layers in reverse.

---

# The TCP/IP Model: The Practical Implementation
The TCP/IP model is a more practical model that is actually used in the Internet. It is a simplified version of the OSI model, with only four layers:

1.  Link Layer: This layer corresponds to the Physical and Data Link layers of the OSI model. It handles the physical transmission of data over a network.
2.  Internet Layer: This layer corresponds to the Network layer of the OSI model. It handles the routing of data packets between networks using IP addresses.
3.  Transport Layer: This layer corresponds to the Transport layer of the OSI model. It provides reliable and ordered delivery of data between applications using TCP or UDP.
4.  Application Layer: This layer corresponds to the Session, Presentation, and Application layers of the OSI model. It provides network services to applications.

### How TCP/IP Works

1.  Encapsulation: When data is sent, each layer adds its own header to the data. This process is called encapsulation. For example, the Application Layer adds an HTTP header, the Transport Layer adds a TCP header, and the Internet Layer adds an IP header.
2.  De-encapsulation: When data is received, each layer removes its corresponding header. This process is called de-encapsulation. The Link layer removes the Ethernet header and trailer, the Internet Layer removes the IP header, the Transport Layer removes the TCP header, and the Application Layer processes the HTTP data.

### TCP/IP in Action: Sending an Email
You compose an email using your email client (e.g., Outlook, Thunderbird).
1.  The email client uses the SMTP protocol (Application Layer) to format the email and prepare it for sending.
2.  TCP (Transport Layer) establishes a connection with the mail server and ensures reliable delivery of the email data.
3.  IP (Internet Layer) routes the email packets across the internet to the mail server.
4.  Ethernet (Link Layer) transmits the packets over the physical network.
The mail server then receives the email, processes it, and forwards it to the recipient's mail server, following a similar process.

#### TCP/IP Header Analysis: Research the structure of a TCP header and an IP header. Identify the key fields in each header and explain their purpose. You can use online resources like Wireshark documentation to explore this.

### Real-World Application
Understanding the OSI and TCP/IP models is crucial for troubleshooting network issues. For example, if you're unable to access a website, you can use the models to systematically diagnose the problem:
1.  Physical Layer: Check the network cable and ensure it's properly connected.
2.  Data Link Layer: Verify that your computer has a valid MAC address and is able to communicate with other devices on the local network.
3.  Network Layer: Check your IP address and ensure that you have a valid gateway configured.
4.  Transport Layer: Use ping to check if you can reach the website's IP address. If you can ping the IP address but cannot access the website in your browser, the problem may be with the application layer.
5.  Application Layer: Check your browser settings and ensure that you have the correct proxy settings configured.
By systematically checking each layer, you can quickly identify the source of the problem and take steps to resolve it.


# TCP/IP Model (From Linux Journey website really good and easy to understand)
	- The OSI model gave birth to what eventually became the TCP/IP model, and this model is actually what the Internet is based on. It is the actual implementation of networking. 
	- The TCP/IP model uses the TCP/IP protocol suite, refer to as TCP/IP. These protocols work together to ^^specify how data should be gathered, addressed, transmitted, and routed through a network.^^ Using the TCP/IP model, we can see how these protocols are used to show the breakdown of how a packet travels through the network.  
		- ## Application Layer
			- The top layer of the TCP/IP model. It determines how your computer's programs (such as your web browser) interface with the transport layer services to view the data that gets sent or received.
				- This layer uses:
					- HTTP (Hypertext Transfer Protocol) - used for webpages on the Internet.
					- SMTP (Simple Mail Transfer Protocol) - electronic mail (email) transmission
		- ## Transport Layer
			- How data will be transmitted, includes checking the correct ports, the integrity of the data, and basically delivering our packets.
				- This layer uses:
					- TCP (Transmission Control Protocol) - reliable data delivery
					- UDP (User Datagram Protocol) - unreliable data delivery
		- ## Network Layer
			- This layer specifies how to move packets between hosts and across networks.
				- This layer uses:
					- IP (Internet Protocol) - Helps route packets from one machine to another.
					- ICMP (Internet Control Message Protocol) - Helps tell us what is going on, such as error messages and debugging information.
		- ## Link Layer
			- This layer specifies how to send data across a physical piece of hardware, such as data traveling through Ethernet, fiber, etc.

# Network Addressing (Linux Journey)
	- When you mail a letter, you must know ^^who it is being sent to^^ and ^^where it is coming from.^^ ^^Packets need the same information.^^ Our hosts and other hosts are identified using MAC (Media Access Control) addresses and IP addresses. To make it easier on us humans, we use hostnames to identify a host.
		- ## MAC Addresses
			- A ^^MAC address^^ is a unique identifier used as a ^^hardware address.^^ This address will never change. When you want to get access to the Internet, 
			  your machine needs to have a device called a ^^network interface card.^^  
			- This network adapter has its own ^^hardware address that's used to identify your machine.^^ A MAC address for an Ethernet device looks something like this: `00:C4:B5:45:B2:43`.
			- MAC addresses are given to network adapters when they are manufactured. Each manufacturer has an Organizationally Unique Identifier (OUI) to identify them as the manufacturer. This OUI is denoted by the first 3 bytes of the MAC address.
			- For example, Dell has `00-14-22`, so a network adapter from Dell could have a MAC address like: `00-14-22-34-B2-C2`.
		- ## IP Addresses
			- An IP address is used to identify a device on a network. They are hardware independent and can vary in syntax depending on if you are using IPv4 or IPv6 .
			- For now, we'll assume you are using IPv4, so a typical IP address would look like: `10.24.12.4`.
			- IP addresses are used with the software side of networking. Anytime a system is connected to the Internet, it should have an IP address. They 
			  can also change if your network changes and are unique to the entire Internet (this isn't always the case once we learn about NAT).  
	- ^^Remember,^^ it takes both software and hardware to move packets across networks, so we have two identifiers for each: MAC (hardware) and IP (software).
		- ## Hostnames
			- One last way to identify your machines is through hostnames. Hostnames take your IP address and allow you to tie that address to a human-readable name. Instead of remembering `192.12.41.4`, you can just remember `myhost.com`.

# Application Layer (Linux Journey)
	- Let's say I wanted to send an email to Patty. We'll go through each of the TCP/IP layers to see this in action.
	- Remember that packets are ^^used to transmit data across networks^^.
	- A ^^packet^^ consists of a header and a payload.
		- ^^The header^^ contains information about where the packet is going and where it came from.
		- ^^The payload^^ is the actual data that is being transferred.
	- As our packet traverses the network, each layer adds a bit of information to the header of the packet.
	- Also, keep in mind that different layers use a different term for our "packet." In the transport layer, we essentially encapsulate our data in a segment, and in the link layer, we refer to this as a frame, but just know that "packet" can be used in regards to the same thing.

	- First, we start off in the application layer. When we send our email through our email client, ^^the application layer will encapsulate this data.^^
	- ^^The application layer talks to the transport layer through a specified port, and through this port, it sends its data.^^ We want to send an email through the application layer protocol SMTP (Simple Mail Transfer Protocol). The data is sent through our transport protocol, which opens a connection to this port (port 25 is used for SMTP). So, we get this data sent through this port, and that data is sent to the Transport layer to be encapsulated into segments.
    
---

# Transport Layer (Linux Journey)
	- ^^The transport layer helps us transfer our data in a way networks can read it.^^
	- It ^^breaks our data into chunks that will be transported and put back together in the correct order.^^ These chunks are known as segments.
	- ^^Segments^^ make it easier to transport data across networks.
    
		- ## Ports
		  background-color:: green
			- Even though we know where we are sending our data ^^via IP addresses,^^ ^^they aren't specific enough to send our data to certain processes or services.^^ Services such as HTTP use a communication channel via ports. If we want to send webpage data, we need to send it over the HTTP port (port 80). In addition to forming segments, ^^the transport layer will also attach the source and destination ports to the segment, so when the receiver gets the final packet it will know what port to use.^^
		- ## UDP

			- There are two popular ^^transport protocols: UDP and TCP.^^
			  We'll briefly discuss UDP and spend most of our time on TCP, since it's the most commonly used.  
			- ^^UDP^^ is not a reliable method of transporting data; in fact, ^^it doesn't really care if you get all of your original data.^^ This may sound terrible, but it does have its uses,
				- such as for media streaming. It's okay if you lose some frames; in return, you get your data a little faster.
		- ## TCP

			- TCP provides a reliable, connection-oriented stream of data.
			- ^^TCP uses ports to send data to and from hosts.^^
			- An application opens up a connection from one port on its host to another port on a remote host. In order to establish the connection, we use the ^^TCP handshake.^^
				- The client (connecting process) sends a SYN segment to the server to request a connection.
				- The server sends the client a SYN-ACK segment to acknowledge the client's connection request.
				- The client sends an ACK to the server to acknowledge the server's connection request.
	- Once this ^^connection is established, data can be exchanged over a TCP connection.^^ The data is sent over in different segments and are tracked with TCP sequence numbers so they can be arranged in the correct order when they are delivered.
	- In our email example, the transport layer attaches the destination port (25) to the source port of the source host.
    
---

# Network Layer (Linux Journey)
	- ^^The Network layer determines^^ ^^the routing of our packets from our source host to a destination host.^^
	- Fortunately, in our example, our packet is only traveling within the same network, but the ^^Internet is made up of many networks.^^
		- These ^^smaller networks that make up the Internet^^ are known as ^^subnets.^^
		- All subnets connect to each other in some way, which is why we are able to get to `https://www.google.com` even though it's on its own network.
		- In regards to our Network layer, know that the ^^IP addresses define the rules to travel to different subnets.^^

	- ^^In the Network layer,^^ it receives the segment coming from the ^^Transport layer^^ and ^^encapsulates this segment in an IP packet, then attaches the IP address of the source host and the IP address of the destination host to the packet header.^^ So at this point, our packet has information about where it is going and where it came from. Now it sends our packet to the physical hardware layer.
    
    - The Network Layer ensures data packets are correctly routed from the source to the destination, even if they are in different networks or subnets. Because direct communication isn't always possible, routers help pass packets along the best available path until they arrive.
    
---

# Link Layer (Linux Journey)
	- At the bottom of the TCP/IP model sits the Link Layer. This layer is ^^hardware-specific.^^
	- In the link layer, ^^our packet is encapsulated once more^^ into something called a frame.
	- The frame header attaches ^^the source^^ and ^^destination MAC addresses of our hosts, checksums, and packet separators^^ so that the receiver can tell when a packet ends.
	- Fortunately, we are on the same network, so our packet won't have to travel too far.

	- First, the link layer attaches my source MAC address to the frame header, but it needs to know Patty's MAC address as well. How does it know that, and how do I find it since it's not on the Internet? We use ARP!
		- ## ARP (Address Resolution Protocol)
			- ^^ARP^^ ^^finds the MAC address associated with an IP address.^^ ARP is ^^used within the same network.^^
			- If Patty was ^^not on the same network,^^ we would ^^use a routing system to determine the next router that would receive the packet,^^ and once we were on the same network, we could use ARP.
			- Once we are on the same network, ^^systems first use the ARP lookup table that stores information about what IP addresses are associated with what MAC address.^^
			- If the value is not there, then ARP is used. ^^Then the system will send a broadcast message to the network using the ARP protocol to find out which host has IP 10.10.1.4. ^^
			- ^^A broadcast message is a special message^^ that is sent to all hosts on a network (aptly named for sending a broadcast). Any machine with the requested IP address will reply with an ARP packet containing the IP address and the MAC address.
			-
	- Now that we have all the necessary data we need—IP address and MAC addresses—our ^^link layer^^ ^^forwards this frame through our network interface card, out to the next device, and finds Patty's network.^^
	- This step is a little more complex than how I just explained it, but we will discuss more details in the Routing course.
	- ^^And there it is: a simple (or not-so-simple) packet traversal down the TCP/IP layer.^^
	- Keep in mind that packets don't travel in a one-way fashion like this. We haven't even gotten to Patty's network yet!
	- ^^When traveling through networks,^^ ^^it requires going through the TCP/IP model at least twice before any data is sent or received.^^
	- In reality, the way this packet looks would be something like this:
		- ## Packet Traversal
			- Pete sends Patty an email: this data gets sent to the transport layer.
			- The transport layer encapsulates the data into a TCP or UDP header to form a segment. The segment attaches the destination and source TCP or UDP port, then the segment is sent to the network layer.
			- The network layer encapsulates the TCP segment inside an IP packet; it attaches the source and destination IP address. Then it routes the packet to the link layer.
			- The packet then reaches Pete's physical hardware and gets encapsulated in a frame. The source and destination MAC addresses get added to the frame.
			- Patty receives this data frame through her physical layer and checks each frame for data integrity, then de-encapsulates the frame contents and sends the IP packet to the network layer.
			- The network layer reads the packet to find the source and destination IP that was previously attached. It checks if its IP is the same as the destination IP, which it is! It de-encapsulates the packet and sends the segment to the transport layer.
			- The transport layer de-encapsulates the segments, checks the TCP or UDP port numbers, and makes a connection to the application layer based 
			  on those port numbers.  
			- The application layer receives the data from the transport layer on the port that was specified and presents it to Patty in the form of the final email message.

# Path of a Packet (Linux Journey)
	- ## Let's look at how a packet travels within its local network
		- First, the local machine will compare the destination IP address to see if it's in the same subnet by looking at its subnet mask.
		- When packets are sent, they need to have a source MAC address, destination MAC address, source IP address, and destination IP address. At this point, we do not know the destination MAC address.
		- To get to the destination host, we use ARP to broadcast a request on the local network to find the MAC address of the destination host.
		- Now the packet can be successfully sent!
        
	- ## Let's see how a packet travels outside its network
		- First, the local machine will compare the destination IP address. Since it's outside of our network, it does not see the MAC address of the destination host. And we can't use ARP because the ARP request is a broadcast to locally connected hosts.
		- So our packet now looks at the routing table. It doesn't know the address of the destination IP, so it sends it out to the default gateway (another router). So now our packet contains our source IP, destination IP, and source MAC; however, we don't have a destination MAC. Remember, MAC addresses are only reached through the same network. So what does it do? It sends an ARP request to get the MAC address of the default gateway.
		- The router looks at the packet and confirms the destination MAC address, but it's not the final destination IP address, so it keeps looking at the routing table to forward the packet to another IP address that can help the packet move along to its destination. Every time the packet moves, it strips the old source and destination MAC addresses and updates the packet with the new source and destination MAC addresses.
		- Once the packet gets forwarded to the same network, we use ARP to find the final destination MAC address.
		- During this process, our packet doesn't change the source or destination IP address.

## IP Packet
The data and information that gets transmitted through networks are known as packets.
- Remember that packets are ^^used to transmit data across networks^^.
- A ^^packet^^ consists of a header and a payload.
	- ^^The header^^ contains information about where the packet is going and where it came from.
	- ^^The payload^^ is the actual data that is being transferred.
- As our packet traverses the network, each layer adds a bit of information to the header of the packet.
- Also, keep in mind that different layers use a different term for our "packet." In the transport layer, we essentially encapsulate our data in a segment, and in the link layer, we refer to this as a frame, but just know that "packet" can be used in regards to the same thing.


    
    
    
    
    



    
    
    
    
