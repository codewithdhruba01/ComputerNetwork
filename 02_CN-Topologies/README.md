# **Computer Network Topologies**

**Network Topology** means how computers or devices are connected in a network.
Topology describes both:

* **Physical structure** (how devices are physically connected)
* **Logical structure** (how data flows)

Different types of network topologies are:

* Point-to-Point Topology
* Bus Topology
* Star Topology
* Ring Topology
* Mesh Topology
* Tree Topology
* Daisy Chain Topology
* Hybrid Topology

---

## **Point-to-Point Topology**

Point-to-Point topology connects **exactly two devices** using a single communication link.
Data travels directly from one device to another without any interruption.
It is the simplest and fastest form of communication.

**Example:** A computer connected to a printer via a cable.

## **Bus Topology**
Bus topology uses **one common communication cable** (called the bus) to connect all devices. All devices share the same cable, so only one device can send data at a time.

**Key point:** If the main bus cable fails, the entire network stops working.

* All devices share **one single communication cable**.
* Only one device can send data at a time.
* If multiple devices send data at the same time → collision happens.
* Uses CSMA/CD protocol or a Bus Master to avoid collisions.
* If the **main shared cable fails**, the whole network fails.
* Both ends of the cable require **terminators**.


## **Star Topology**

In Star topology, all devices are connected to a **central device** such as a hub, switch, or router.
All communication happens through this central device.

**Key point:** If the central device fails, the whole network fails.

Central device may be:

* **Layer-1 device:** Hub or Repeater
* **Layer-2 device:** Switch or Bridge
* **Layer-3 device:** Router or Gateway


## **Ring Topology**
In Ring topology, each device is connected to **two other devices**, forming a circular path.
Data travels around the ring in one or both directions until it reaches its destination.

**Key point:** If any one device fails, the entire ring breaks (unless backup ring is used).

* Each device is connected to **two other devices**, forming a closed loop.
* Data travels in one direction or both directions depending on the design.
* Adding a new device is easy — only one extra cable is needed.
* If one device fails → whole ring breaks (unless dual ring backup is used).


## **Mesh Topology**

Mesh topology provides **multiple connections** between devices.
Each device may connect to multiple devices or **to every device** .

**Two types:**

### **1. Full Mesh**

* Every device is connected to **every other device**.
* Very reliable — no single point of failure.
* Requires many cables → expensive.

### **2. Partial Mesh**

* Only selected devices are fully connected.
* Others have limited connections.
* Used where reliability is required but cost needs to be controlled.

Devices in Mesh also act as **relay nodes** for others.


## **Tree Topology (Hierarchical Topology)**

Tree topology is a combination of **Star + Bus topology**.
Devices are arranged in **multiple layers**: Core, Distribution, and Access layers.

* Common in LANs.

* Divided into three layers:

  * **Core Layer** – The top/root of the network
  * **Distribution Layer** – Middle layer that connects core and access
  * **Access Layer** – Bottom layer where user devices connect

* Failure at the root affects the entire network.

* Every connection is a potential point of failure.


## **Daisy Chain Topology**
Devices are connected **in a straight line**, one after another.
Each device is connected to the next in the chain.

**Key point:** If one link fails, the chain breaks into two parts.

> If both ends are connected, it becomes a **Ring Topology**.

* Devices are connected **in a straight line**, one by one.
* Only end devices connect to one device; middle devices connect to two.
* Each link is a single point of failure.
* If both end devices are connected, it becomes a Ring Topology.


## **Hybrid Topology**
Hybrid topology is a mix of **two or more** topologies such as Star + Ring + Bus.
It combines the advantages of all included topologies.

**Example:** Modern WAN networks and the Internet.

* Mix of two or more topologies (Star + Ring + Bus etc.)
* Used in large networks, including WANs.
* Most reliable and flexible.
* **Internet** is the biggest example of a hybrid topology.

---

# **Point-to-Point (PPP) Network Topology**
Point-to-Point Protocol (PPP) is a communication protocol used at the **Data Link Layer** to transfer data between **two directly connected devices**.
It is a **byte-oriented protocol** and is widely used in broadband connections where data transfer needs to be fast and reliable.
PPP sends data in the form of **frames** and is also defined in **RFC 1661**.

## **Services Provided by PPP**
PPP provides several important services while creating and managing a point-to-point link:

* **Defines frame format** for sending data.
* **Defines how to establish a link** between two devices and exchange data.
* **Explains how network layer data** should be encapsulated inside the frame.
* **Provides authentication rules** for verifying the communicating devices.
* **Assigns addresses** needed for network communication.
* **Supports communication over multiple links**.
* **Supports multiple network layer protocols**, giving flexibility.


## **Components of PPP**
PPP is a layered protocol with **three main components**:

### 1. **Encapsulation Component**
Used for converting the datagram into a format that can be transmitted over the physical layer.

### 2. **Link Control Protocol (LCP)**

Responsible for:

* Establishing
* Configuring
* Testing
* Maintaining
* Terminating

the point-to-point link.
LCP also handles negotiation for options like link quality, authentication, etc.

### 3. **Authentication Protocols (AP)**

Used to authenticate the endpoints before communication.

PPP uses two authentication protocols:

* **PAP (Password Authentication Protocol)**
  Sends username and password for authentication (less secure).

* **CHAP (Challenge Handshake Authentication Protocol)**
  More secure; uses a challenge-response mechanism.


## **Network Control Protocols (NCPs)**

NCPs help configure different network-layer protocols over PPP.
Each supported protocol has its own NCP.

Common NCPs include:

* IPCP – Internet Protocol Control Protocol
* OSINLCP – OSI Network Layer Control Protocol
* IPXCP – Internetwork Packet Exchange Control Protocol
* DNCP – DECnet Phase IV Control Protocol
* NBFCP – NetBIOS Frames Control Protocol
* IPV6CP – IPv6 Control Protocol


## **PPP Frame Format**
PPP uses a **byte-oriented frame structure**, where each field is made of one or more bytes.

### The fields of a PPP frame are:

* **Flag (1 byte)**
  Marks the start and end of a frame. Bit pattern: `01111110`

* **Address (1 byte)**
  Used for broadcast; fixed value: `11111111`

* **Control (1 byte)**
  Usually set to a constant value: `11000000`

* **Protocol (1–2 bytes)**
  Specifies the type of payload inside the frame.

* **Payload (variable length)**
  Actual data coming from the network layer.
  Maximum length: **1500 bytes** (negotiable).

* **FCS (2 or 4 bytes)**
  Frame Check Sequence for error detection (uses CRC).

## **Byte Stuffing in PPP Frame**

Byte stuffing is used when the payload accidentally contains a **flag byte** (01111110).
To avoid confusion, PPP inserts an **escape byte (01111101)** before any data byte that looks like the flag or escape byte.

When the receiver gets the frame:

* It recognizes the escape byte
* Removes it,
* And restores the original data.

---

# **Bus Topology**

Bus Topology is one of the simplest types of network topologies where **all devices are connected to a single central cable**, known as the **bus** or **backbone cable**.
Every device shares this same communication line to send and receive data.

> When a device sends data, the message travels through this central cable, and **all devices receive it**, but only the device with the correct address accepts it.

## **How Bus Topology Works**

* A single long cable connects all computers and network devices.
* Devices tap into the cable using connectors.
* Data is transmitted in **one direction** at a time.
* **Terminators** are placed at both ends of the bus cable to absorb signals and prevent bounce-back.

## **Features of Bus Topology**

* All devices share **one communication line**.
* Uses techniques like **CSMA/CD** to avoid collisions.
* Only one device can send data at a time.
* Easy to connect a new device by simply adding it to the bus.

## **Advantages of Bus Topology**

* Very simple and easy to install.
* Cost-effective because it uses less cable compared to other topologies.
* Good for small networks like home networks or small offices.


## **Disadvantages of Bus Topology**

* If **main bus cable fails**, the whole network stops working.
* Performance decreases when many devices send data at the same time.
* Troubleshooting cable faults is difficult.
* Not suitable for large networks.

**Examples**

* Early Ethernet networks
* Small office networks using coaxial cable
