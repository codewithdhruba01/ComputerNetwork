# **Transport Layer**

## **What is Transport Layer?**

Transport Layer is the **fourth layer** of the OSI model and provides **end-to-end communication** between applications running on different hosts. It ensures reliable data transfer and manages flow control, error recovery, and segmentation.

**Position:** Layer 4 (Between Session and Network Layer)
**Main Function:** End-to-end communication and data transfer
**Data Unit:** Segments (TCP) / Datagrams (UDP)
**Key Protocols:** TCP, UDP

---

## **Functions of Transport Layer**

### **1. Segmentation and Reassembly**
- Breaks large messages into smaller segments
- Reassembles segments at the destination
- Each segment has sequence numbers for ordering

### **2. End-to-End Communication**
- Establishes logical connection between applications
- Uses port numbers to identify applications
- Provides process-to-process delivery

### **3. Error Detection and Recovery**
- Detects corrupted segments using checksums
- Retransmits lost or corrupted segments
- Ensures reliable data delivery (in TCP)

### **4. Flow Control**
- Prevents sender from overwhelming receiver
- Uses sliding window mechanism
- Manages buffer space at receiver

### **5. Congestion Control**
- Prevents network congestion
- Adjusts transmission rate based on network conditions
- Uses algorithms like TCP Tahoe, Reno, New Reno

---

## **TCP (Transmission Control Protocol)**

TCP is a **connection-oriented**, **reliable** transport protocol that provides:
- Reliable data delivery
- Ordered delivery of segments
- Error detection and correction
- Flow control and congestion control

### **TCP Header Format**
```
0                   1                   2                   3
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Sequence Number                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Acknowledgment Number                      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Data |           |U|A|P|R|S|F|                               |
| Offset| Reserved  |R|C|S|S|Y|I|            Window             |
|       |           |G|K|H|T|N|N|                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Checksum            |         Urgent Pointer        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                            Data                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

### **Key TCP Header Fields**

#### **1. Source/Destination Port (16 bits each)**
- Identifies sending/receiving application
- Port range: 0-65535
- Well-known ports: 0-1023 (HTTP:80, FTP:21, etc.)

#### **2. Sequence Number (32 bits)**
- Identifies position of data in byte stream
- Used for ordering and duplicate detection
- Initial sequence number chosen randomly

#### **3. Acknowledgment Number (32 bits)**
- Next expected sequence number
- ACK = Last received sequence number + 1

#### **4. Data Offset (4 bits)**
- Size of TCP header in 32-bit words
- Minimum: 5 (20 bytes), Maximum: 15 (60 bytes)

#### **5. Control Flags (6 bits)**
- **URG**: Urgent pointer field is valid
- **ACK**: Acknowledgment field is valid
- **PSH**: Push data immediately to application
- **RST**: Reset connection
- **SYN**: Synchronize sequence numbers
- **FIN**: No more data to send

#### **6. Window Size (16 bits)**
- Amount of data receiver can accept
- Used for flow control
- Maximum: 65535 bytes (can be scaled)

#### **7. Checksum (16 bits)**
- Error detection for header + data
- Calculated using one's complement

#### **8. Urgent Pointer (16 bits)**
- Points to urgent data when URG flag is set

---

## **TCP Connection Establishment (3-Way Handshake)**

### **Phase 1: SYN**
```
Client → Server: SYN (seq=x)
```
- Client sends SYN segment with initial sequence number x
- SYN flag = 1, ACK flag = 0

### **Phase 2: SYN-ACK**
```
Server → Client: SYN-ACK (seq=y, ack=x+1)
```
- Server responds with SYN-ACK
- Server's sequence number y, acknowledges client's x+1
- SYN=1, ACK=1

### **Phase 3: ACK**
```
Client → Server: ACK (seq=x+1, ack=y+1)
```
- Client acknowledges server's sequence number
- Connection established
- SYN=0, ACK=1

**Total Time:** 1.5 RTT (Round Trip Time)

---

## **TCP Connection Termination (4-Way Handshake)**

### **Phase 1: FIN**
```
Client → Server: FIN (seq=x)
```
- Client wants to close connection
- FIN=1, ACK=0

### **Phase 2: ACK**
```
Server → Client: ACK (ack=x+1)
```
- Server acknowledges FIN
- Connection enters CLOSE_WAIT state

### **Phase 3: FIN**
```
Server → Client: FIN (seq=y)
```
- Server sends its own FIN
- Server enters LAST_ACK state

### **Phase 4: ACK**
```
Client → Client: ACK (ack=y+1)
```
- Client acknowledges server's FIN
- Connection closed after TIME_WAIT (2 MSL)

**Total Time:** 2 RTT + 2 MSL (Maximum Segment Lifetime)

---

## **TCP States**

### **Client States:**
1. **CLOSED**: No connection
2. **SYN_SENT**: SYN sent, waiting for SYN-ACK
3. **ESTABLISHED**: Connection established
4. **FIN_WAIT_1**: FIN sent, waiting for ACK
5. **FIN_WAIT_2**: ACK received, waiting for FIN
6. **TIME_WAIT**: Waiting for 2 MSL, then CLOSED

### **Server States:**
1. **CLOSED**: No connection
2. **LISTEN**: Waiting for connection requests
3. **SYN_RECEIVED**: SYN received, SYN-ACK sent
4. **ESTABLISHED**: Connection established
5. **CLOSE_WAIT**: FIN received, waiting for application close
6. **LAST_ACK**: FIN sent, waiting for ACK

---

## **TCP Flow Control (Sliding Window)**

### **How it Works:**
1. **Receiver advertises window size** in TCP header
2. **Sender can send up to window size** bytes without waiting for ACK
3. **Window slides forward** as ACKs are received
4. **Prevents buffer overflow** at receiver

### **Types of Sliding Window:**
- **Go-Back-N**: Retransmit all unacknowledged packets
- **Selective Repeat**: Retransmit only missing packets

### **Silly Window Syndrome**
- Occurs when small amounts of data are sent
- Solution: Clark's algorithm and Nagle's algorithm

---

## **TCP Congestion Control**

### **Congestion Window (cwnd)**
- Limits amount of data sender can transmit
- Independent of receiver's advertised window

### **Congestion Control Algorithms**

#### **1. TCP Tahoe (1988)**
- **Slow Start**: cwnd doubles every RTT
- **Congestion Avoidance**: cwnd increases linearly
- **Fast Retransmit**: Retransmit after 3 duplicate ACKs
- **Timeout**: cwnd reset to 1 MSS

#### **2. TCP Reno (1990)**
- **Fast Recovery**: After fast retransmit, cwnd halved
- **Fast Retransmit + Fast Recovery**

#### **3. TCP New Reno (1996)**
- Improved fast recovery for multiple losses

#### **4. TCP BBR (2016)**
- Bottleneck Bandwidth and Round-trip propagation time
- Uses bandwidth estimation instead of loss

### **Congestion Control Phases**
1. **Slow Start**: cwnd = 1 → 2 → 4 → 8... (exponential)
2. **Congestion Avoidance**: cwnd increases linearly (+1 per RTT)
3. **Fast Retransmit**: Send duplicate ACKs to trigger retransmission
4. **Fast Recovery**: Reduce cwnd but don't go to slow start

---

## **UDP (User Datagram Protocol)**

UDP is a **connectionless**, **unreliable** transport protocol that provides:
- Fast, simple data transmission
- No connection establishment
- No reliability guarantees
- Minimal overhead

### **UDP Header Format**
```
0                   1                   2                   3
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|            Length             |           Checksum            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                            Data                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

### **UDP Header Fields**
- **Source Port**: Sending application (optional)
- **Destination Port**: Receiving application
- **Length**: Total length including header (minimum 8 bytes)
- **Checksum**: Error detection (optional in IPv4, mandatory in IPv6)

---

## **TCP vs UDP Comparison**

| Feature | TCP | UDP |
|---------|-----|-----|
| **Connection** | Connection-oriented | Connectionless |
| **Reliability** | Reliable | Unreliable |
| **Ordering** | Guaranteed | Not guaranteed |
| **Speed** | Slower | Faster |
| **Header Size** | 20-60 bytes | 8 bytes |
| **Flow Control** | Yes | No |
| **Congestion Control** | Yes | No |
| **Error Recovery** | Yes | No |
| **Use Cases** | HTTP, FTP, Email | DNS, DHCP, VoIP, Streaming |

---

## **Port Numbers**

### **Well-Known Ports (0-1023)**
- **20/21**: FTP (File Transfer Protocol)
- **22**: SSH (Secure Shell)
- **23**: Telnet
- **25**: SMTP (Simple Mail Transfer Protocol)
- **53**: DNS (Domain Name System)
- **67/68**: DHCP (Dynamic Host Configuration Protocol)
- **80**: HTTP (Hypertext Transfer Protocol)
- **110**: POP3 (Post Office Protocol)
- **143**: IMAP (Internet Message Access Protocol)
- **443**: HTTPS (HTTP Secure)
- **3389**: RDP (Remote Desktop Protocol)

### **Registered Ports (1024-49151)**
- Assigned by IANA for specific services

### **Dynamic/Private Ports (49152-65535)**
- Used by client applications
- Ephemeral ports

---

## **Transport Layer in TCP/IP Model**

In TCP/IP model, Transport Layer is called **Host-to-Host Layer** and includes:
- **TCP**: For reliable, connection-oriented communication
- **UDP**: For fast, connectionless communication
- **SCTP**: Stream Control Transmission Protocol (used in VoIP)

---

## **Error Detection and Correction**

### **Checksum Calculation**
- TCP/UDP use one's complement checksum
- Sum all 16-bit words
- Take one's complement of sum
- If result is 0, no error detected

### **Sequence Numbers**
- Used for detecting duplicate or out-of-order segments
- 32-bit numbers wrap around

### **Timeouts and Retransmissions**
- **RTT Estimation**: Calculate round trip time
- **Retransmission Timeout (RTO)**: When to retransmit
- **Karn's Algorithm**: Handle retransmission ambiguity

---

## **Quality of Service (QoS)**

### **TCP QoS Features**
- **Reliability**: Guaranteed delivery
- **Throughput**: Controlled by congestion control
- **Delay**: Minimized through pipelining
- **Jitter**: Controlled through sequencing

### **UDP QoS Features**
- **Low Latency**: No connection setup
- **Low Overhead**: Small header
- **Multicasting**: Support for one-to-many communication

---

## **Interview Questions & Answers**

### **Q1: What is the main function of Transport Layer?**
**Ans:** Transport Layer provides end-to-end communication between applications on different hosts. It handles segmentation, error recovery, flow control, and ensures reliable data delivery.

### **Q2: Explain TCP 3-way handshake.**
**Ans:** TCP 3-way handshake establishes connection:
1. Client sends SYN (seq=x)
2. Server responds with SYN-ACK (seq=y, ack=x+1)
3. Client sends ACK (seq=x+1, ack=y+1)
Connection established after 1.5 RTT.

### **Q3: What is the difference between TCP and UDP?**
**Ans:** TCP is connection-oriented, reliable, slower with overhead. UDP is connectionless, unreliable, faster with minimal overhead. TCP used for HTTP/FTP, UDP for DNS/DHCP/VoIP.

### **Q4: Explain TCP flow control.**
**Ans:** Flow control prevents sender from overwhelming receiver using sliding window. Receiver advertises window size, sender transmits up to that limit, window slides as ACKs received.

### **Q5: What is congestion control in TCP?**
**Ans:** Congestion control prevents network congestion by adjusting transmission rate. Uses slow start (exponential increase), congestion avoidance (linear increase), and algorithms like Tahoe, Reno.

### **Q6: What happens during TCP connection termination?**
**Ans:** TCP uses 4-way handshake:
1. Client sends FIN
2. Server sends ACK, then FIN
3. Client sends ACK
4. Connection closes after TIME_WAIT (2 MSL)

### **Q7: Explain TCP fast retransmit.**
**Ans:** When receiver gets out-of-order segment, it sends duplicate ACKs. Sender retransmits after receiving 3 duplicate ACKs, without waiting for timeout.

### **Q8: What is TCP sequence number?**
**Ans:** 32-bit number identifying byte position in data stream. Used for ordering segments, detecting duplicates, and acknowledging received data.

### **Q9: What are the TCP states?**
**Ans:** Key states: CLOSED, LISTEN, SYN_SENT, SYN_RECEIVED, ESTABLISHED, FIN_WAIT_1, FIN_WAIT_2, CLOSE_WAIT, LAST_ACK, TIME_WAIT.

### **Q10: Explain TCP window scaling.**
**Ans:** TCP window scaling allows window sizes > 65535 bytes. Scale factor negotiated during connection setup, multiplies advertised window by 2^scale_factor.

### **Q11: What is UDP used for?**
**Ans:** UDP used for applications requiring speed over reliability: DNS queries, DHCP, VoIP, video streaming, online gaming.

### **Q12: Explain TCP checksum calculation.**
**Ans:** TCP uses one's complement checksum. Sum all 16-bit words, add carry to sum, take one's complement. If result is 0 at receiver, no error detected.

### **Q13: What is TIME_WAIT state in TCP?**
**Ans:** TIME_WAIT (2 MSL) ensures all segments are delivered and prevents delayed segments from previous connection affecting new connections.

### **Q14: Explain TCP Reno vs Tahoe.**
**Ans:** Tahoe: On timeout, reset cwnd to 1, enter slow start. Reno: On 3 duplicate ACKs, halve cwnd, enter fast recovery (don't go to slow start).

### **Q15: What is TCP MSS (Maximum Segment Size)?**
**Ans:** MSS is maximum amount of data TCP can send in one segment. Negotiated during connection setup, typically 1460 bytes for Ethernet.

---

## **Key Points for Interviews**

1. **Transport Layer is Layer 4** in OSI model
2. **TCP is connection-oriented, UDP is connectionless**
3. **TCP provides reliability**, UDP doesn't
4. **3-way handshake** for TCP connection establishment
5. **Sliding window** for flow control
6. **Congestion control** prevents network congestion
7. **TCP header is 20-60 bytes**, UDP header is 8 bytes
8. **Port numbers** identify applications (0-65535)
9. **TCP states** are important (ESTABLISHED, TIME_WAIT, etc.)
10. **Checksum** for error detection in both TCP and UDP

---

## **Quick Revision Table**

| Concept | TCP | UDP |
|---------|-----|-----|
| **Connection** | Connection-oriented | Connectionless |
| **Reliability** | Reliable | Unreliable |
| **Speed** | Slower | Faster |
| **Header Size** | 20-60 bytes | 8 bytes |
| **Flow Control** | Yes | No |
| **Congestion Control** | Yes | No |
| **Error Recovery** | Yes | No |
| **Use Cases** | HTTP, FTP, Email | DNS, DHCP, VoIP |
| **Ordering** | Guaranteed | Not guaranteed |
| **Handshaking** | 3-way | None |

---

## **Common Interview Scenarios**

### **Scenario 1: Web Browsing (HTTP)**
- Uses TCP (reliable delivery needed)
- Port 80 (HTTP) or 443 (HTTPS)
- Connection established via 3-way handshake

### **Scenario 2: Video Streaming**
- Uses UDP (speed > reliability)
- Tolerates some packet loss
- Real-time requirements

### **Scenario 3: DNS Query**
- Uses UDP (fast response needed)
- Small query/response packets
- Retransmission handled by application

### **Scenario 4: File Transfer (FTP)**
- Uses TCP (reliability critical)
- Large data transfers
- Error recovery essential
