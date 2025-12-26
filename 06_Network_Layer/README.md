# Network Layer

## Table of Contents
1. [Introduction](#introduction)
2. [Functions of Network Layer](#functions-of-network-layer)
3. [IP Addressing](#ip-addressing)
4. [IPv4 Addressing](#ipv4-addressing)
5. [IPv6 Addressing](#ipv6-addressing)
6. [Subnetting](#subnetting)
7. [Supernetting (CIDR)](#supernetting-cidr)
8. [Routing](#routing)
9. [Routing Algorithms](#routing-algorithms)
10. [Routing Protocols](#routing-protocols)
11. [ARP and RARP](#arp-and-rarp)
12. [ICMP](#icmp)
13. [IGMP](#igmp)
14. [Fragmentation and Reassembly](#fragmentation-and-reassembly)
15. [Network Layer Devices](#network-layer-devices)
16. [NAT (Network Address Translation)](#nat-network-address-translation)
17. [Interview Questions & Answers](#interview-questions--answers)

---

## Introduction

**Network Layer** (Layer 3) is the third layer in the OSI model. It is responsible for logical addressing and routing of data packets from source to destination across multiple networks. The main protocol at this layer is IP (Internet Protocol).

### Key Characteristics:
- Provides logical addressing (IP addresses)
- Enables internetworking between different networks
- Handles routing of packets
- Manages network congestion
- Provides quality of service (QoS)

---

## Functions of Network Layer

### 1. **Logical Addressing**
- Assigns IP addresses to devices for identification
- Enables communication between devices on different networks

### 2. **Routing**
- Determines optimal path for data packets
- Uses routing tables and algorithms to find best route

### 3. **Packet Forwarding**
- Moves packets from one network to another
- Makes decisions based on destination IP address

### 4. **Fragmentation and Reassembly**
- Breaks large packets into smaller fragments
- Reassembles fragments at destination

### 5. **Congestion Control**
- Prevents network overload
- Manages traffic flow to avoid congestion

### 6. **Error Handling and Diagnostics**
- Reports delivery errors
- Provides network diagnostic information

---

## IP Addressing

IP addressing is the method of assigning unique identifiers to devices on a network.

### Types of IP Addresses:

### 1. **Unicast Address**
- Identifies single device
- Most common type of IP address

### 2. **Multicast Address**
- Identifies group of devices
- Used for one-to-many communication

### 3. **Broadcast Address**
- Identifies all devices on network
- Used for one-to-all communication

### 4. **Anycast Address**
- Identifies group of devices but delivers to nearest one
- Used for load balancing and redundancy

---

## IPv4 Addressing

IPv4 uses 32-bit addresses written in dotted decimal notation.

### Address Classes:

| Class | Range | Default Subnet Mask | Networks | Hosts per Network |
|-------|-------|---------------------|----------|-------------------|
| A | 0.0.0.0 - 127.255.255.255 | 255.0.0.0 (/8) | 126 | 16,777,214 |
| B | 128.0.0.0 - 191.255.255.255 | 255.255.0.0 (/16) | 16,384 | 65,534 |
| C | 192.0.0.0 - 223.255.255.255 | 255.255.255.0 (/24) | 2,097,152 | 254 |
| D | 224.0.0.0 - 239.255.255.255 | N/A | Multicast | N/A |
| E | 240.0.0.0 - 255.255.255.255 | N/A | Experimental | N/A |

### Special IPv4 Addresses:

| Address | Purpose | Example |
|---------|---------|---------|
| Network Address | Identifies network | 192.168.1.0/24 |
| Broadcast Address | All hosts on network | 192.168.1.255 |
| Loopback Address | Local host testing | 127.0.0.1 |
| Private Addresses | Internal networks | 192.168.x.x, 10.x.x.x, 172.16-31.x.x |

---

## IPv6 Addressing

IPv6 uses 128-bit addresses written in hexadecimal notation.

### Address Format:
- 8 groups of 4 hexadecimal digits separated by colons
- Example: `2001:0DB8:85A3:0000:0000:8A2E:0370:7334`

### Address Types:

### 1. **Unicast**
- Identifies single interface
- **Global Unicast**: Internet-routable
- **Link-Local**: Local network only (FE80::/10)
- **Unique Local**: Private networks (FC00::/7)

### 2. **Multicast**
- Group communication (FF00::/8)
- Well-known addresses for specific functions

### 3. **Anycast**
- Group of interfaces, packet delivered to nearest

### IPv6 Features:
- **Larger Address Space**: 2^128 addresses
- **Simplified Header**: Fixed 40-byte header
- **Auto-configuration**: Stateless address auto-configuration (SLAAC)
- **Security**: Built-in IPsec support
- **No Broadcast**: Uses multicast instead

---

## Subnetting

Subnetting divides a large network into smaller sub-networks.

### Why Subnetting?
- **Efficient IP Usage**: Reduces IP address waste
- **Network Security**: Isolates network segments
- **Performance**: Reduces broadcast domains
- **Management**: Easier network administration

### Subnetting Process:

**Example:** Divide 192.168.1.0/24 into 4 subnets

1. **Determine subnet bits needed:**
   - 2^n ≥ number of subnets
   - 2^2 = 4 subnets → 2 bits borrowed

2. **Calculate new subnet mask:**
   - Original: 255.255.255.0 (/24)
   - New: 255.255.255.192 (/26)

3. **Calculate subnet ranges:**

| Subnet | Network Address | Host Range | Broadcast |
|--------|----------------|------------|-----------|
| 1 | 192.168.1.0/26 | 192.168.1.1-62 | 192.168.1.63 |
| 2 | 192.168.1.64/26 | 192.168.1.65-126 | 192.168.1.127 |
| 3 | 192.168.1.128/26 | 192.168.1.129-190 | 192.168.1.191 |
| 4 | 192.168.1.192/26 | 192.168.1.193-254 | 192.168.1.255 |

### Variable Length Subnetting (VLSM)
- Allows different subnet masks within same network
- More efficient IP address allocation
- Requires classless routing protocols

---

## Supernetting (CIDR)

CIDR (Classless Inter-Domain Routing) combines multiple networks into larger supernetwork.

### CIDR Notation:
- Written as IP/prefix-length
- Example: 192.168.0.0/22 represents 1024 addresses

### Benefits:
- **Route Aggregation**: Reduces routing table size
- **Efficient Addressing**: Eliminates class boundaries
- **Hierarchical Addressing**: Better address allocation

### CIDR Calculation:

**Example:** Combine 192.168.0.0/24, 192.168.1.0/24, 192.168.2.0/24, 192.168.3.0/24

1. **Common bits:** All start with 192.168.
2. **Differing bits:** Last octet (8 bits)
3. **Supernet:** 192.168.0.0/22 (covers 1024 addresses)

---

## Routing

Routing is the process of selecting paths in a network for data packets.

### Types of Routing:

### 1. **Static Routing**
- Manually configured routes
- **Advantages:** Secure, no routing protocol overhead
- **Disadvantages:** Not scalable, manual updates required

### 2. **Dynamic Routing**
- Routes learned automatically via protocols
- **Advantages:** Automatic updates, scalable
- **Disadvantages:** Protocol overhead, convergence time

### 3. **Default Routing**
- Route for all destinations not in routing table
- Usually points to next-hop router toward internet

### Routing Table Components:
- **Destination Network**
- **Subnet Mask**
- **Next-Hop Address**
- **Outgoing Interface**
- **Metric** (cost/distance)
- **Administrative Distance** (trustworthiness)

---

## Routing Algorithms

### 1. **Distance Vector Algorithms**
- Uses Bellman-Ford algorithm
- Exchanges routing tables with neighbors
- **Examples:** RIP, IGRP

**Working:**
- Each router maintains distance to all destinations
- Shares table with neighbors periodically
- Updates based on neighbor information

**Problems:**
- **Count to Infinity**: Slow convergence
- **Routing Loops**: Can occur during topology changes

### 2. **Link State Algorithms**
- Uses Dijkstra's algorithm
- Maintains complete topology map
- **Examples:** OSPF, IS-IS

**Working:**
- Each router floods link state information
- Builds complete network topology
- Calculates shortest path to all destinations

**Advantages:**
- Faster convergence
- Loop-free routing
- Better scalability

### 3. **Path Vector Algorithm**
- Used in inter-domain routing
- Carries path information in routing updates
- **Example:** BGP

---

## Routing Protocols

### Interior Gateway Protocols (IGP):

### 1. **RIP (Routing Information Protocol)**
- Distance vector protocol
- Uses hop count as metric (max 15 hops)
- Updates every 30 seconds
- **Versions:** RIPv1 (classful), RIPv2 (classless)

### 2. **OSPF (Open Shortest Path First)**
- Link state protocol
- Uses cost as metric (bandwidth-based)
- Supports VLSM and route summarization
- **Areas:** Hierarchical design for scalability

### 3. **EIGRP (Enhanced Interior Gateway Routing Protocol)**
- Cisco proprietary, advanced distance vector
- Uses composite metric (bandwidth, delay, reliability, load)
- Supports unequal cost load balancing
- Faster convergence than RIP

### Exterior Gateway Protocol (EGP):

### 4. **BGP (Border Gateway Protocol)**
- Path vector protocol for internet routing
- Uses AS (Autonomous System) numbers
- Policies control route selection
- **Versions:** BGP-4 (current standard)

---

## ARP and RARP

### ARP (Address Resolution Protocol)
Converts IP addresses to MAC addresses.

**Working:**
1. Host broadcasts ARP request: "Who has IP 192.168.1.1?"
2. Target host replies with its MAC address
3. Requester caches the mapping

**ARP Cache:**
- Stores IP-MAC mappings temporarily
- Prevents repeated ARP requests
- Timeout: Usually 4 hours (Windows), 20 minutes (Linux)

### RARP (Reverse Address Resolution Protocol)
Converts MAC addresses to IP addresses.

**Use Case:**
- Diskless workstations booting from network
- DHCP has largely replaced RARP

**Working:**
1. Host broadcasts RARP request with its MAC
2. RARP server responds with IP address

---

## ICMP

ICMP (Internet Control Message Protocol) handles error reporting and network diagnostics.

### ICMP Message Types:

| Type | Name | Description |
|------|------|-------------|
| 0 | Echo Reply | Response to Echo Request (ping) |
| 3 | Destination Unreachable | Cannot reach destination |
| 4 | Source Quench | Congestion control (obsolete) |
| 5 | Redirect | Better route available |
| 8 | Echo Request | Ping request |
| 9 | Router Advertisement | Router discovery |
| 10 | Router Solicitation | Router discovery |
| 11 | Time Exceeded | TTL expired |
| 12 | Parameter Problem | Invalid header field |
| 13 | Timestamp Request | Time synchronization |
| 14 | Timestamp Reply | Time synchronization |

### Common ICMP Tools:
- **Ping**: Tests connectivity (Echo Request/Reply)
- **Traceroute**: Shows path to destination
- **Pathping**: Combines ping and traceroute

---

## IGMP

IGMP (Internet Group Management Protocol) manages multicast group membership.

### Versions:
- **IGMPv1**: Basic join/leave functionality
- **IGMPv2**: Added leave messages
- **IGMPv3**: Source-specific multicast

### Working:
1. **Join**: Host sends Membership Report to join multicast group
2. **Query**: Router periodically queries for active members
3. **Leave**: Host sends Leave Group message
4. **Prune**: Router stops forwarding if no members

### Multicast Address Ranges:
- **224.0.0.0 - 224.0.0.255**: Local network control
- **224.0.1.0 - 238.255.255.255**: User multicast
- **239.0.0.0 - 239.255.255.255**: Administrative scope

---

## Fragmentation and Reassembly

### Why Fragmentation?
- Different networks have different MTU (Maximum Transmission Unit)
- Ethernet: 1500 bytes, Token Ring: 4096 bytes
- Packets larger than MTU must be fragmented

### IPv4 Fragmentation:
- **Identification**: Same for all fragments of same packet
- **Fragment Offset**: Position of fragment in original packet
- **More Fragments (MF) Flag**: 1 for all fragments except last
- **Don't Fragment (DF) Flag**: Prevents fragmentation

### Fragmentation Process:
```
Original Packet: 4000 bytes
MTU: 1500 bytes

Fragment 1: Offset 0, MF=1, Data: 1480 bytes
Fragment 2: Offset 1480, MF=1, Data: 1480 bytes
Fragment 3: Offset 2960, MF=0, Data: 1040 bytes
```

### IPv6 Fragmentation:
- **No fragmentation at intermediate routers**
- **Path MTU Discovery**: Source determines minimum MTU along path
- **Fragmentation only at source** (if required)

---

## Network Layer Devices

### 1. **Router**
- Connects multiple networks
- Makes forwarding decisions based on IP addresses
- Maintains routing tables
- Can perform NAT, firewall functions

### 2. **Layer 3 Switch**
- High-performance router
- Hardware-based routing
- Used in enterprise networks
- Combines switching and routing

### 3. **Multilayer Switch**
- Operates at multiple OSI layers
- Can perform routing, switching, firewall functions
- More expensive but higher performance

---

## NAT (Network Address Translation)

NAT translates private IP addresses to public IP addresses.

### Types of NAT:

### 1. **Static NAT**
- One-to-one mapping
- Used for servers requiring fixed public IP

### 2. **Dynamic NAT**
- Many-to-many mapping using pool of addresses
- Assigns available public IP from pool

### 3. **PAT (Port Address Translation)**
- Many-to-one mapping
- Uses port numbers to differentiate connections
- Most common type (hides entire network behind single IP)

### Advantages:
- **Conserves IP addresses**
- **Security**: Hides internal network structure
- **Easy reconfiguration**

### Disadvantages:
- **Breaks end-to-end connectivity**
- **Application issues** (some protocols don't work through NAT)
- **Performance overhead**

---

## Interview Questions & Answers

### Basic Questions

**Q1: What is the main function of Network Layer?**
- **Answer:** The Network Layer is responsible for logical addressing, routing, and forwarding of packets across multiple networks. It provides end-to-end connectivity between devices on different networks using IP addresses.

**Q2: Explain the difference between IPv4 and IPv6.**
- **Answer:** IPv4 uses 32-bit addresses (4.3 billion addresses) while IPv6 uses 128-bit addresses (340 undecillion addresses). IPv6 has simplified header, built-in security (IPsec), auto-configuration, and eliminates NAT. IPv4 is widely deployed but IPv6 solves address exhaustion.

**Q3: What is subnetting and why is it used?**
- **Answer:** Subnetting divides a large network into smaller sub-networks. It's used to:
  - Efficiently use IP addresses
  - Improve network security by isolating segments
  - Reduce broadcast domains
  - Make network management easier

**Q4: Explain ARP and its working.**
- **Answer:** ARP (Address Resolution Protocol) maps IP addresses to MAC addresses. When a device wants to communicate, it broadcasts an ARP request asking "Who has IP X?" The device with that IP responds with its MAC address, which gets cached for future use.

### Intermediate Questions

**Q5: What is CIDR and why is it important?**
- **Answer:** CIDR (Classless Inter-Domain Routing) allows flexible subnetting by using variable-length subnet masks. It's important because:
  - Eliminates class boundaries for efficient addressing
  - Enables route aggregation to reduce routing table sizes
  - Supports hierarchical addressing structure
  - Prevents IP address waste

**Q6: Explain the difference between distance vector and link state routing.**
- **Answer:**
  - **Distance Vector**: Each router shares its routing table with neighbors. Uses Bellman-Ford algorithm. Examples: RIP, IGRP. Slower convergence, prone to routing loops.
  - **Link State**: Each router shares link state information to build complete topology map. Uses Dijkstra's algorithm. Examples: OSPF, IS-IS. Faster convergence, more scalable.

**Q7: What is NAT and why is it used?**
- **Answer:** NAT (Network Address Translation) translates private IP addresses to public IP addresses. It's used to:
  - Conserve public IP addresses
  - Provide security by hiding internal network structure
  - Allow multiple devices to share single public IP
  - Enable easy network reconfiguration

**Q8: Explain ICMP and its common uses.**
- **Answer:** ICMP (Internet Control Message Protocol) handles error reporting and network diagnostics. Common uses:
  - Ping (Echo Request/Reply) for connectivity testing
  - Traceroute for path discovery
  - Destination Unreachable for error reporting
  - Time Exceeded for TTL expiration

### Advanced Questions

**Q9: How does OSPF work? Explain its advantages over RIP.**
- **Answer:** OSPF uses link state routing where each router floods link state advertisements (LSAs) to build a complete topology map. It uses Dijkstra's algorithm to calculate shortest paths. Advantages over RIP:
  - Faster convergence
  - Supports VLSM and route summarization
  - Uses cost metric instead of hop count
  - Scalable hierarchical design with areas
  - Loop-free routing

**Q10: Explain BGP and its role in internet routing.**
- **Answer:** BGP (Border Gateway Protocol) is the routing protocol used between autonomous systems on the internet. It uses path vector algorithm and carries complete path information in routing updates. BGP makes routing decisions based on policies rather than just technical metrics. It's crucial for internet routing because:
  - Connects different organizations' networks
  - Allows policy-based routing decisions
  - Prevents routing loops through AS path information
  - Supports route aggregation and filtering

**Q11: What is VLSM and why is it useful?**
- **Answer:** VLSM (Variable Length Subnet Mask) allows different subnet masks within the same network class. It's useful because:
  - Enables more efficient IP address allocation
  - Allows subnets of different sizes based on actual need
  - Reduces IP address waste
  - Requires classless routing protocols (RIPv2, OSPF, EIGRP)

**Q12: Explain IPv6 address types and their purposes.**
- **Answer:**
  - **Unicast**: Identifies single interface (Global unicast for internet, Link-local for local network, Unique local for private networks)
  - **Multicast**: Delivers to group of interfaces (replaces IPv4 broadcast)
  - **Anycast**: Delivers to nearest interface in group (used for load balancing and redundancy)
  - IPv6 eliminates broadcast addresses, using multicast instead.

### Scenario-Based Questions

**Q13: You need to design a network for 1000 users. How would you approach IP addressing and subnetting?**
- **Answer:** For 1000 users:
  - Use private IP range (192.168.0.0/22 = 1024 addresses)
  - Subnet into smaller segments based on departments/locations
  - Use VLSM for efficient allocation
  - Plan for growth (20-30% extra addresses)
  - Consider using DHCP for dynamic assignment
  - Implement proper DNS and network documentation

**Q14: A company is running out of public IP addresses. What solutions would you recommend?**
- **Answer:** Solutions for IP address exhaustion:
  - Implement NAT/PAT to share public IPs
  - Migrate to IPv6 for abundant address space
  - Use CIDR for efficient public IP allocation
  - Implement network address planning and reclamation
  - Consider cloud migration with provider's IP management

**Q15: Explain how traceroute works at network layer.**
- **Answer:** Traceroute works by sending packets with incrementally increasing TTL values:
  - First packet: TTL=1, expires at first router, router sends ICMP Time Exceeded
  - Second packet: TTL=2, expires at second router, and so on
  - Each router in path responds with ICMP Time Exceeded message
  - Shows complete path, round-trip time to each hop
  - Helps identify network bottlenecks and routing issues

---

## Key Takeaways

1. **Network Layer** provides logical addressing and routing across networks
2. **IPv4/IPv6** addressing schemes enable device identification and communication
3. **Subnetting** and **CIDR** enable efficient IP address utilization
4. **Routing protocols** (RIP, OSPF, BGP) determine optimal paths for data
5. **ARP** maps IP to MAC addresses, **ICMP** handles errors and diagnostics
6. **NAT** conserves IP addresses and provides security
7. **Fragmentation** handles different network MTU requirements

---

*This comprehensive guide covers all major topics in Network Layer with detailed explanations and interview preparation questions.*
