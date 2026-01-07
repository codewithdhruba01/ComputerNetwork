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

## Types of ALOHA Protocol
There are **two main versions** of the ALOHA Protocol:

1. Pure ALOHA  
2. Slotted ALOHA  

## Pure ALOHA
In Pure ALOHA:
- Transmission time is **continuous**
- A station can transmit data at any time
- There is no concept of fixed time slots

### Drawbacks
- High probability of collisions
- Low channel utilization
- Maximum throughput ≈ **18%**

## Slotted ALOHA
Slotted ALOHA is an improved version of Pure ALOHA.

### Working
- The shared channel is divided into **equal time slots**
- A station can transmit data only at the **beginning of a time slot**
- Random transmissions are avoided

### When does collision occur?
- When multiple stations attempt to transmit at the beginning of the same slot

### Advantages
- Reduced number of collisions
- Better channel utilization
- Maximum throughput ≈ **36%**

---

## Comparison: Pure ALOHA vs Slotted ALOHA

| Feature | Pure ALOHA | Slotted ALOHA |
|-------|------------|---------------|
| Time | Continuous | Slot-based |
| Transmission | Anytime | At slot start |
| Collision | High | Lower |
| Efficiency | Low (~18%) | Higher (~36%) |
| Synchronization | Not required | Required |


## Key Points
- ALOHA is a simple but inefficient protocol
- Slotted ALOHA performs better than Pure ALOHA
- These protocols laid the foundation for modern networking techniques
- Modern networks mostly use **CSMA/CD** and **CSMA/CA**


## Conclusion
The ALOHA Protocol played an important role in the development of computer
networks. Although it is not widely used today, it provided the basic concepts
of **multiple access communication** that influenced modern network protocols.
