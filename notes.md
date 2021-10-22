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