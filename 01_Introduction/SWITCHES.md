# **Switches in Computer Networks**

Switches are networking devices that operate at **Layer 2 (Data Link Layer)** of the OSI model.
Their main job is to **connect devices** in a network and use **packet switching** to send, receive, or forward data frames.

A switch has many **ports** where computers and devices are plugged in.

When a data frame arrives at any port:

1. The switch reads the **destination MAC address**
2. Performs necessary checks
3. Sends the frame to the **correct device**

Switches support:

* **Unicast** (one-to-one communication)
* **Multicast** (one-to-many)
* **Broadcast** (one-to-all)


# **Features of Switches**

* Switch works at **Layer 2** (Data Link Layer).
* It is an **intelligent device** and works like a multiport bridge.
* Uses **MAC addresses** to send packets to the correct device.
* Uses **packet switching** for forwarding data.
* Supports **unicast, multicast, and broadcast** communication.
* Works in **full duplex mode**, meaning data moves in both directions at the same time (no collisions).
* Switches are **active devices**, contain software and management features.
* Can perform **error checking** before sending data.
* Usually have **24 or 48 ports**.


# **Types of Switches**

Switches are broadly divided into **four types**:

1. **Unmanaged Switch**
2. **Managed Switch**
3. **LAN Switch**
4. **PoE Switch**

## **1. Unmanaged Switch**

* Cheapest and simplest switches
* Common in **home networks** and small offices
* **Plug-and-play** → automatically start working
* No configuration required
* Used when more devices need to be added quickly
* Do not provide control or monitoring features

## **2. Managed Switch**

* More expensive and used in **large and complex networks**
* Can be **configured** for advanced control
* Support **QoS (Quality of Service)** features
* Provide higher security, better monitoring, and control
* Offer high scalability → used in growing organizations
* Managed using protocols like **SNMP (Simple Network Management Protocol)**

## **3. LAN Switch**

* Used inside the **Local Area Network** of an organization
* Also called **Ethernet switches** or **Data switches**
* Help reduce network congestion
* Provide proper bandwidth allocation
* Ensure no overlapping of data packets in the network


## **4. PoE Switch**

* **PoE = Power over Ethernet**
* Sends **power + data** through the same Ethernet cable
* Used in PoE Gigabit Ethernet networks
* Useful for devices like:

  * IP cameras
  * Wireless access points
  * VoIP phones
* Makes installation simple because no separate power cable needed
