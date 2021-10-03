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