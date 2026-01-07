# Network Protocols

## Introduction
Network Protocols are a set of rules and standards that define how data is
**transmitted, received, and processed** over a computer network.
They ensure smooth and reliable communication between different devices,
regardless of their hardware or software differences.

Network protocols operate at different layers of the **OSI Model** and make
data communication reliable, secure, and efficient.

## What is the ALOHA Protocol?
The **ALOHA Protocol** is a **Multiple Access Protocol** used for data
transmission over a shared communication channel.

- It operates in the **MAC (Medium Access Control) sublayer**
  of the **Data Link Layer** in the OSI Model
- Multiple stations share a single communication channel
- Data is transmitted through a **multi-point transmission channel**

## Working of the ALOHA Protocol
- Each station transmits data without checking whether the channel is idle or busy
- If the channel is idle, the frame is transmitted successfully
- If two or more stations transmit at the same time, a **collision** occurs
- When a collision happens:
  - The frames are discarded
  - The sender waits for a random amount of time
  - The frame is retransmitted
- This process continues until the frame is transmitted successfully
