# TCP/IP Model

The **TCP/IP Model** stands for **Transmission Control Protocol / Internet Protocol**.
It is the **fundamental communication model of the Internet** and was developed **before the OSI model**.
The TCP/IP model explains **how data is sent, routed, and received** over networks like the Internet.

> Unlike the OSI model (7 layers), the TCP/IP model has **4 layers**, and each layer has a specific role.


## Layers of TCP/IP Model

### Application Layer

* Topmost layer of TCP/IP
* Provides **network services to user applications**
* Combines **Application, Presentation, and Session layers** of OSI
* Common protocols:

  * **HTTP** – web browsing
  * **FTP** – file transfer
  * **SMTP / POP3** – email
  * **DNS** – domain name resolution

**Example:** Opening a website in a browser.


### Transport Layer

* Ensures **end-to-end communication** between devices
* Responsible for **data delivery, error control, and flow control**

**Protocols used:**

* **TCP** – reliable, connection-oriented (used in web, email)
* **UDP** – fast, connectionless (used in video streaming, gaming)
* **SCTP** – message-oriented transport protocol

**Example:** TCP ensures a webpage loads correctly.


### Internet Layer (Network Layer)

* Responsible for **logical addressing and routing**
* Decides **how data moves from source to destination across networks**

**Protocols used:**

* **IP (IPv4, IPv6)**
* **ICMP** (error reporting)
* **Routing protocols**

**Example:** Finding the best path to reach another network.


### Host-to-Network (Link) Layer

* Lowest layer of TCP/IP
* Handles **physical transmission of data**
* Equivalent to **Physical + Data Link layers** of OSI
* Deals with hardware, MAC addresses, cables, and NICs

**Example:** Sending bits over Ethernet or Wi-Fi.


## TCP/IP vs OSI (Quick Interview Point)

| OSI Model         | TCP/IP Model         |
| ----------------- | -------------------- |
| 7 Layers          | 4 Layers             |
| Theoretical model | Practical model      |
| Not used directly | Used by the Internet |


## Inshort

> **The TCP/IP model is a four-layer network model used by the Internet to transmit data reliably from source to destination.**


## Why TCP/IP is Important?

* Backbone of the **Internet**
* Platform-independent
* Highly **scalable and reliable**
* Used in **real-world networking**
