# The internet
- Interconnected with communication links and packet switches
  - Two types of packet switches
    - Routers: Directs traffic
    - Link-layer switches: Connects multiple devices to one router
- End system/host: Consumer devices connected to the internet
- Access network
  - Connects the end system to the first router
  - The optical fiber from the central office is split at the splitter to many homes
- Packet switching
  - Store-and-forward transmission
    - Packets are buffered in a queue
    - Packet loss occurs if packets arrive when the buffer is full
- Circuit switching
  - Resources are reserved between end systems
  - Circuit switched links may be multiplexed with frequency-division multiplexing or time-division multiplexing
  - Packet switching may be more bandwidth efficient than circuit switching
- Forwarding table: Maps destination addresses to outbound links

# Tiered network
- Tier-1 ISP
  - Has global coverage and connects with many access ISPs
  - Internet Exchange Point (IXP) meeting point of multiple ISPs
- Point of presence: Group of routers in the provider network where customer ISPs can connect to
- Regional ISP group together many access ISPs
- Content-provider networks
  - A private connections between data centers of a company
  - Connects to tier-1 networks

# Delay
- Nodal processing delay
  - Time needed to read the packet header
- Queuing delay
  - Packets are queued at a router
- Transmission delay
  - Time needed to transmit the packet
- Propagation delay
  - Time needed for bits to travel through a link
- The total delay is the total nodal delay
- Traffic intensity
  - La/R where L=packet bits, a=average packets/sec, R=transmission rate
  - If traffic intensity is greater than 1, queuing delay increases and packets may be dropped
  - If traffic intensity is 0, there is 0 queuing delay
- Throughput: transfer rate expressed in bits/sec

# Internet protocol stack
- Application
  - Network applications and application-layer protocols
  - HTTP
  - A packet of information in the application layer is a message
- Transport
  - Controls flow of packets
  - TCP
  - A packet of transport information is referred to a segment
- Network
  - Moves data between hosts
  - A packet is called a datagram
- Link
  - Routes datagrams through routers
  - A packet is called a frame
- Physical
  - Bits are converted into signals to send through links

# Network security
- Types of denial-of-service attacks
  - Vulnerability attack: Exploits vulnerabilities
  - Bandwidth flooding: Floods the host with packets
  - Connection flooding: Establishes a large number of open TCP connections
- Distributed DoS: Attacker controls compromised hosts to attack a target
- Packet sniffer: A receiver that copies packets in transit
- IP spoofing: Creating packets that contain a false source address
  - End-point authentication: A mechanism that authenticates the source address

# Application layer
- Reliable data transfer
  - A guarantee of packet validity and delivery
  - Ensures protection against data loss and data corruption
  - TCP ensures reliable data transfer with handshakes
- Loss tolerant application: Media that is useful even with a small amount of data loss
- Bandwidth-sensitive application
  - Streaming services that rely on a certain bandwidth requirement
  - Elastic application: Applications that work with any bandwidth, such as e-mail
- Persistent connection: TCP requests and responses are sent over the same TCP connection
- HTTP/2 reduces latency by multiplexing request and responses over a single TCP connection so that HOL blocking does not occur

# SMTP procedure
1. Alice composes an email
2. Alice's user agent sends the mail to her mail server, and is placed in the message queue
3. The SMTP client retrieves the message from the queue and opens a TCP connection to Bob's mail server
4. SMTP handshake occurs. The SMTP client sends Alice's message to Bob's server.
5. Bob's mail server places the message in Bob's mailbox
6. Bob's user agent retrieves the message from the mailbox

# Domain Name System (DNS)
- DNS is used for: host aliasing, mail server aliasing, load distribution
- Types of DNS servers
  - Root DNS: Provides the IP addresses of the TLD servers corresponding to TLDs (.com, .gov, etc.)
  - TLD server: Provides DNS servers for authoritative DNS servers
  - Authoritative DNS server: A name server that maps hostnames belonging to organizations to smaller subdomains
  - Local DNS server: Acts as a cache
- Iterative vs recursive queries: An iterative query means the local DNS server follows mappings to resolve a full query. For a recursive query, a chain of DNS servers gets the full mapping for the local DNS server's behalf
- Resource record
  - (Name, Value, Type, TTL)
  - If type=A, name is hostname and value is IP address
    - Maps hostname to IP
  - If type=NS, name is domain name and value is hostname of DNS server that can obtain IP addresses for hosts in that domain
    - Routes DNS queries
  - If type=CNAME, name is the origin name and value is the alias name
    - Redirect
  - If type=MX, name is mapped to an alias value
    - Mail server

# Video streaming
- Dynamic Adaptive Streaming over HTTP (DASH): Adaptive bitrate streaming protocol
- Content Distribution Network (CDN)

# Transport layer
- Logical communication: The apparent perspective that communication between two hosts are direct. In reality, there are multiple relays along the physical structure.
- The transport layer provides logical communication, whereas the network layer deals with physical communication
- Socket
  - Different doors of a network process that data can pass through. AKA port.
  - Segments are multiplexed by adding the source and destination info to the header, and demultiplexed with the header info
  - 0-1023 are well-known port numbers and are reserved

# UDP
- UDP characteristics
  - Finer application level control over data control
  - No connection establishment and no handshakes
  - No connection state. Compared to TCP, which does maintain connection state.
  - Small packet header overhead
- UDP segment structure
  - 16-bit source port #
  - 16-bit destination port #
  - 16-bit segment length (Including header)
  - 16-bit checksum for header and data
  - Payload data
  
# Reliable data transfer protocol
- A protocol that has ensures reliable transfer of data across a network that may be subject to data loss and corruption
- It doesn't mean that all packets are sent without fail; it means that all such failures are reported as errors
- Checksums and ACK acknowledgement enables:
  - Error detection
  - Receiver feedback: A success or error response
  - Retransmission after an error response
- A sequence number adds clarification to which packet an ACK is for
- A countdown timer ensures that a lost packet can be sent again
- Pipelined data transfer
  - In a stop-and-wait protocol, the utilization of time and bandwidth is low
    - U_sender = L/R / (RTT + L/R) where RTT = return trip time
  - By sending multiple packets before ACK, utilization is higher
  - Go-back-N protocol: If an ACK for sequence N is not returned before timeout, the Nth packet is sent again, regardless of if an ACK for N+M is received
  - Selective repeat protocol: The sequence number of each ACK is marked. If there is an unmarked sequence number after timeout, that packet is sent again. Marked packets are never sent again.

# TCP
- Connection-oriented: A handshake must occur before the main message is transmitted
- TCP segment
  - A chunk of data of a data stream
  - TCP segment header structure
    - 16-bit source port
    - 16-bit destination port
    - 32-bit sequence number field: Byte number of segment
    - 32-bit acknowledgement number field: Byte number of next expected segment
    - 16-bit receive window: Number of windows that the sender can store
    - 4-bit Header length field
    - Variable-length options field
    - 6-bit flag field: ACK, RST, SYN, FIN, PSH, URG
- Receivers send cumulative acknowledgements, or acknowledgements of the last sequence number received
- Handling of out-of-order segments is up to the implementation, but implementations typically have a buffer to store out-of-order segments
- Piggybacking: Delaying the ACK to send it back in the next segment
- Timeout interval is calculated by keeping an estimated RTT
  - Estimated RTT changes based on the sampled RTT
  - Exponential weighted moving average: Formula to calculate estimated RTT
  - Timeout interval is set above the estimated RTT
    - Timeout interval = Estimated RTT + 4 * DevRTT
- Fast retransmit: A receiver may send two duplicate ACKs after an out-of-order segment. The sender sends back the missing segment immediately, rather than waiting for timeout.
- Slow-start: Since the receiving side's buffer and bandwidth capacity is unknown, the segment rate is slow at first
- Flow-control: Matches the rate of data transfer for the sender and receiver so that the receiver's buffer doesn't overflow, using the receive window field
- Congestion control
  - With a higher rate of segments, bigger buffers, higher bandwidth, and other network resources are necessary
  - Solution
    - Additive increase, multiplicative decrease (AIMD)
    - Increase segment rate until timer rate or triple ACK, which means a segment was dropped
    - A dropped segment indicates congestion
    - On segment loss, the segment rate is decreased
    - Segment rate may be halved (TCP Tahoe) or decreased by one (TCP Reno)
  - TCP CUBIC: Increases segment rate by logarithmic growth to send more segments until the limit
  - Explicit congestion notification
- Explicit congestion notification: A bit in the segment header that a router can set to indicate that it is experiencing congestion
- TCP Vegas: Measurement of congestion based on RTT, not segment loss

# Network layer
- Although data in the network layer are datagrams, they are also referred to as packets
- Forwarding
  - Router-local action of sending a packet to the appropriate output destination
  - Managed inside the data plane
- Routing
  - Network-wide process of determining end-to-end paths
  - Managed by the control plane
- Forwarding table: A mapping of IP ranges to output link
- Software-defined networking: An approach to routing where software in the control plane sets forwarding tables, instead of through human management
- The network layer only guarantees best-effort service
  - The network layer does not guarantee in-order delivery or reliability

# Router
- Input port
  - Physical end termination of incoming link
  - Decapsulates (decodes) packets
  - Uses forwarding table to get output link interface
  - Longest prefix matching rule: Find forwarding table entry with the longest matching prefix
  - The packet is sent to the switching fabric
- Switching fabric
  - Connects input ports to output ports
  - Memory switching
    - Old routing mechanism where a buffer stores and delivers the packet
    - Limited to memory IO speed
  - Bus switching
    - The output is attached to a packet's header and sent along a bus
    - Only one packet can cross the bus at a time
  - Interconnect network
    - A crossbar switch that delivers the packet without blocking
- Output port
  - Queues packets
    - Size of buffer needed is B = RTT * C / sqrt(N) where C = link bandwidth and N = number of TCP flows
  - Transmits packet to outgoing link
  - Output order can be by FIFO or by priority of packet
  - Weighted fair queuing discipline: A round-robin method of serving one packet per each class of priority
- Routing processor
  - Performs control-plane functions
  - Communicates with remote controller to receive forwarding tables

# Internet Protocol
- IPv4 header
  - Version (Always 4)
  - Internet Header Length: Size of header
  - Differentiated Services Code Point (DSCP): Specifies type of service, such as real-time or non-real-time service
  - Explicit Congestion Notification (ECN): Congestion control
  - Total length: Packet size
  - Identification, flags, fragment offset: Identifies fragmented datagrams, which are datagrams broken into smaller datagrams that are reassembled at the destination
  - Time to live: A number that limits a datagram's lifetime. Each router decrements this number by 1. When it hits 0, the datagram is discarded.
  - Protocol: Identifies transport layer protocol, such as 6 for TCP.
  - Header checksum: For error correction of header. Each router must recompute the checksum since a value may change. UDP and TCP have separate checksums.
  - 32-bit source IP address
  - 32-bit destination IP address
  - Options: A rarely used field for setting the behavior of the datagram.
  - Payload
- Subnet
  - A subdivision of an IP network
  - Subnet mask: Used to specify the size of the subnet
  - CIDR: Specifies prefix and mask
  - Classful addressing: 8-, 16-, and 24-bit subnet addresses. These classes were either too small or too large for organizations, and it led to a rapid depletion of unallocated addresses.
- The ICANN allocates blocks of addresses to ISPs. The ISPs further divides their block to individual organizations.
- IP addresses in an organization can be manually distributed to hosts, or Dynamic Host Configuration Protocol (DHCP) can be used to do this automatically.
- DHCP protocol
  - DHCP discover message is sent via UDP from the connecting client to the broadcast address 255.255.255.255
  - DHCP offer message is broadcasted to 255.255.255.255, containing the proposed address for the client (YIADDR), network mask, and address lease time
  - Client broadcasts a DHCP request for the address
  - DHCP acknowledges the request
- Network address translation (NAT)
  - The port number is used as an extension to an IP address
  - A client is assigned a private IP address in the address space 10.0.0.0/24
  - When a client sends a packet, a NAT router replaces the source address with a public address and a unique port number according to a NAT translation table
  - Incoming packets have the destination address and port rewritten to the private IP address
- IPv6 header
  - Version (Always 6)
  - Traffic class: Type of service
  - Flow: Identifies a stream of packets, such as for a media stream
  - Payload length
  - Next header: Identifies the transport layer protocol of the payload
  - Hop limit: Replaces TTL field in IPv6
  - 128-bit source address
  - 128-bit destination address
  - Payload
- IPv6 removes the fragmentation, checksum, and options fields
- IPv6 transition
  - Tunneling: Packaging IPv6 datagrams into IPv6 datagrams so that IPv4 routers can pass IPv6 datagrams

# Generalized forwarding
- Instead of destination-based forwarding, generalized forwarding is a layer 3 switch that uses header fields of different protocols in different layers
- OpenFlow flow table
  - Implementation of software-defined networking
  - Match-plus-action forwarding table
  - Each entry contains:
    - A set of header field values: Matched to the packet
    - A set of counters: Can include number of matched packets and time since last update
    - A set of actions to take: For example, forwarding packet to an output port, drop the packet, modify header fields
- Some use cases of SDNs are routers, load balancers, and firewalls
- Middlebox
  - An intermediary box performing functions different from those of an IP router
  - Some examples: NAT translation, security services, load balancers

# Network control plane
- Two approaches to router control
  - Per-router control
    - A routing algorithm runs in every router individually
  - Logically centralized control
    - A centralized controller distributes forwarding tables to all routers
    - Control agent: An agent in a router that communicates with the central controller

# Routing algorithms
- Static routing algorithm: Routing tables change very slowly, often because they are manually set
- Dynamic routing algorithm: Routing tables are changed often due to automated systems
- Load-sensitive algorithm
- Link costs vary depending on the level of congestion
  - Modern routing algorithms are load-insensitive
- Link-state routing algorithm
  - Used for centralized control because all link costs are known by the controller
  - Dijkstra's algorithm is an implementation of LS routing
    - Worst-case complexity of O(|E| + |V|log(|V|))
- Distance-vector routing
  - Iterative, asynchronous, and distributed
  - For per-router controllers
  - Bellman-Ford equation
    - Worst-case complexity of O(|V||E|)
  - The solution to the Bellman-Ford equation provides the forwarding tables
  - Count-to-infinity problem
    - A routing loop where a disconnected link causes routers to increment the cost of that link to infinity
    - Can be avoided with poisoned reverse

# Open Shortest Path First (OSPF)
- Intra-autonomous system routing protocol
  - Autonomous system: A group of routers that are under the same administrative control
  - Routers store path information for their own autonomous system
- OSPF
  - Open standard used for intra-AS routing
  - Uses Dijkstra's algorithm
  - Each router is given a graph of the AS, and each router computes the shortest paths to all subnets
  - Authenticates packets

# Border Gateway Protocol (BGP)
- Inter-autonomous system routing protocol
- Purpose
  - Obtain prefix reachability information
  - Determine best routes to prefixes
- Types of routers in autonomous systems
  - Internal router: Connects only to hosts and routers within the AS
  - Gateway router: Connects to internal routers of its own AS and routers of other ASs
- Routing information is exchanged through BPG connections which are TCP-based
- External BGP (eBGP): A BGP connection that spans two ASs
- Internal BGP (iBGP): A BGP connection within the same AS
- Routing information contains BGP attributes
  - AS-PATH
    - A list of ASNs that the advertisement has passed through
    - A router adds their ASN to the front of the list and passes it on
    - If a router sees its own ASN, the information is discarded as it looped back
  - NEXT-HOP
    - IP address of the router interface that begins the AS-PATH
- BGP route selection priority
  1. Local preference value
    - A policy decision by the AS to send packets to a certain router
  2. The route with the shortest AS-PATH is selected
  3. Hot potato routing
    - Packets are passed to the AS with the lowest immediate cost
- IP-anycast
  - Different hosts have the same IP addresses
  - If a router sees different routes to the same address, the best route is picked
  - It is useful for CDNs, as routers will pick the fastest CDN
  - Also used for DNS servers

# Software-defined networking (SDN)
- Key characteristics of the SDN architecture
  - Traditional routers only read the IP address from a packet, but SDN flow tables consider many more header fields of packets
  - The data plane consists of switches, and the control plane consists of servers and software to manage flow tables
  - Controllers hold network state information and control the switches
  - Network-control applications receives state information from the controller and computes routing paths and flow tables
  - The SDN can be programmed through APIs
- The controller API is the northbound interface, and the switch API is the southbound interface
- OpenFlow
  - OpenFlow is a protocol in which the control plane communicates with the data plane
  - The controller can send the following messages:
    - Configuration: sets configuration parameters
    - Modify-state: Adds or deletes flow entries and port properties
    - Read-state: Collects statistics and counter values
    - Send-packet: Specifies a message to send
  - Switches can send the following messages:
    - Flow-removed: A flow table has been removed
    - Port-status: A port status was changed
    - Packet-in: A packet that does not match a table entry is sent for additional processing
- Example SDN interaction
  1. The link between switches s1 and s2 fails. Port-status message is sent to inform the controller of the failure.
  2. The SDN controller notifies the link-state manager
  3. The network-control application receives notification of the link-state change
  4. The link-state manager computes new least-cost paths
  5. The flow table manager creates flow tables
  6. The flow table manager sends modify-state messages to update flow tables

# Internet Control Message Protocol (ICMP)
- ICMP is for error reporting, such as unreachable hosts
- ICMP is part of the network layer
- Ping and traceroute use ICMP

# Network management
- Managing server: Operated by network managers and controls the network devices
- Managed device: Network equipment such as hosts, routers, and switches
- Data
  - Configuration data: Device information explicitly configured by the network manager
  - Operational data: Information that a device collects as it operates, such as the list of immediate neighbors
  - Device statistics: Status indicators and counts
- Network management agent: Software running in the managed device that communicates with the managing server
- Network management protocol: A protocol that allows communication between the managing server and managed devices

# Simple Network Management Protocol (SNMP)
- Application layer protocol for conveying network-management control and information messages
- Used to set and retrieve MIB object values on a managed device
- Also used for sending trap messages (notifications) to a managing server
- Some uses for MIB objects are: the number of datagrams discarded, number of carrier sense errors, and the version of a software

# Network Configuration Protocol (NETCONF)
- Similar to SNMP, NETCONF is used for setting and retrieving operational and configuration data
- XML-based RPC
  - YANG: Data modeling language used for NETCONF
- Commands are applied to a set of devices
- The difference between SNMP is that SNMP sets values on individual devices, whereas NETCONF sets the configuration of the network as a whole

# Link layer
- Node: A device that runs a link-layer protocol
- Data is transmitted in link-layer frames
- Link layer services
  - Framing: Data is packaged in frames
  - Link access: A MAC protocol manages frame transmission
  - Reliable delivery: Even though TCP ensures reliability, nodes can resend frames between links to avoid the need for end-to-end retransmission
  - Error detection and correction: Error detection bits are included in frames to fix bit errors
- Network adapter/network interface controller (NIC): Hardware that handles link layer responsibilities

# Error detection and correction
- Parity bit: 1 bit included with a string to detect errors. Checks that the total number of 1-bits in a string is even or odd.
- Forward error correction: The ability to detect and correct errors without retransmission
- Internet checksum
  - The sum of 16-bit words of the data and the checksum should be zero
  - Used for IP packets and TCP and UDP messages
- Cyclic redundancy check (CRC)
  - Better algorithm than a checksum for detecting burst errors

# Multiple access link
- Point-to-point link: A link that consists of a single sender and a single receiver
- Broadcast link: A link that has multiple sending and receiving nodes
- A multiple access protocol regulates transmission by nodes in a broadcast channel
- Channel partitioning protocols
  - Time-division multiplexing
  - Frequency-division multiplexing
  - Code division multiple access (CDMA)
    - Each node is assigned a code to encode data
    - Nodes can transmit simultaneously and receivers can still receive data
    - Used in older mobile phone standards
  - Random access protocol
    - Nodes transmit frames at full rate, but when there is a collision, frames are retransmitted after a random delay
    - Binary exponential backoff: The random delay to retransmit increases by twice the max delay of the previous transmission attempt
    - Carrier sense multiple access with collision detection (CSMA/CD)
      - Carrier sensing: A node listens for ongoing transmissions before transmitting to avoid collision
      - Even if carrier sensing is used, channel collisions occur because of channel propagation delay
      - Obsolete method for Ethernet 
  - Taking-turns protocol
    - Polling protocol: A master node polls each transmitter for a certain number of frames
    - Has a polling delay
    - Avoids collisions
    - Token-passing protocol: Nodes exchange tokens to decide who can transmit
  - Data Over Cable Service Interface Specification (DOCSIS)
    - For sending data over cable
    - Uses FDM for data transmission, and TDM to assign slots
    - New modems can send a request for a slow using random access protocol

# Switched local area network
- MAC address
  - A device-specific and (usually) permanent address
  - 6 bytes or 48 bits
  - Used in link-layer to address frames
  - Broadcast address is FF-FF-FF-FF-FF-FF
- Address Resolution Protocol (ARP)
  - Translates IP addresses to MAC addresses
- Ethernet
  - Link and physical layer standards
  - An Ethernet frame contains:
    - Preamble: A wake-up and sync signal
    - Destination address: MAC address of destination adapter
    - Source address: MAC address of sender
    - Type: Indicates the payload protocol
    - Data: The payload
    - CRC: Checksum for frame
  - Ethernet has various flavors, such as 10, 100, 1000 MB/s, 10, 40 GB/s
- Link-layer switch
  - Filtering: A switch function that determines whether a frame should be forwarded or dropped
  - Switch table: A mapping of MAC address to switch interface
  - A switch can take one of three actions for a frame:
    - If there is no entry for the destination address, that frame is broadcasted
    - If the entry for the destination address has the same interface as the one the switch received the frame from, the frame is discarded
    - If the entry for the destination address is not the same interface, the frame is forwarded to the interface
  - Switches learn which MAC address is connected to which interface
    - Link-layer switches works automatically, without manual configuration
    - If no frames are received from an address within a given period of time, the entry is deleted
  - In contrast to a hub-and-spoke LAN architecture, a mesh of switches reduces the chances of collisions
  - Switches allow different Ethernet protocols to work together
  - Routers are network-layer (and above) devices, whereas switches are link-layer
- Virtual local area network (VLAN)
  - A VLAN is a sub-division of a switched LAN that functions like a single isolated network 
  - The ports on a switch are partitioned into VLANs
  - A VLAN trunk can carry traffic across the VLANs
  - A frame can contain a VLAN tag which identifies VLAN that the frame belongs to

# Multiprotocol label switching (MPLS)
- Improves forwarding speed of routers by attaching a fixed-length label to packets
- Packets can be forwarded based on the label and not the IP headers
- Instead of finding the longest-prefix match, the router only finds the matching label from a lookup table
- MPLS enables multiple-path routing
- MPLS can be used to implement VPNs

# Data center networking
- Blade: A modular server computer
- Top of rack (TOR) switch: A switch connecting all blades in one rack
- Border router: A router that connects the data center network to the public internet
- Tier-2 switches connect groups of tier-3 TOR switches and tier-1 switches connect tier-2 switches
- Load balancers operate at the tier-1 level
- To enable fast communication within a data center network, switches are highly interconnected so that there is no bottleneck link