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

