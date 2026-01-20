# Network Algorithms

This directory contains resources and explanations of fundamental algorithms used in computer networking. These algorithms are the backbone of efficient data transmission, routing, and traffic management in the Internet and local networks.

## Table of Contents
1. [Routing Algorithms](#routing-algorithms)
    - [Dijkstra's Algorithm (Shortest Path)](#1-dijkstras-algorithm-shortest-path)
    - [Bellman-Ford Algorithm (Distance Vector)](#2-bellman-ford-algorithm-distance-vector)
    - [Flooding](#3-flooding)
2. [Congestion Control Algorithms](#congestion-control-algorithms)
    - [Leaky Bucket Algorithm](#1-leaky-bucket-algorithm)
    - [Token Bucket Algorithm](#2-token-bucket-algorithm)

---

## Routing Algorithms

Routing algorithms determine the specific choice of route for each packet from its source to its destination.

### 1. Dijkstra's Algorithm (Shortest Path)
**Type:** Link State Routing Algorithm

Dijkstra's algorithm is used to find the shortest path from a starting node to all other nodes in a graph. In networking, it allows a router to build a complete map of the network (Link State) and calculate the best path to every other router.

**Key Steps:**
1.  Initialize distances to all nodes as infinite, except the source (0).
2.  Mark all nodes as unvisited.
3.  Select the unvisited node with the smallest tentative distance (current node).
4.  Calculate the distance to its unvisited neighbors. If the new distance is smaller than the previously recorded distance, update it.
5.  Mark the current node as visited.
6.  Repeat until all nodes are visited or the destination is reached.

### 2. Bellman-Ford Algorithm (Distance Vector)
**Type:** Distance Vector Routing Algorithm

Bellman-Ford computes shortest paths from a single source vertex to all of the other vertices in a weighted digraph. Unlike Dijkstra, it can handle graphs with negative edge weights (though network links rarely have negative costs).

**Mechanism:**
*   Each router maintains a table (vector) of minimum distances to every other node.
*   Routers periodically share their vectors with **immediate neighbors**.
*   **Update Rule:** If a neighbor offers a shorter path to a destination, the router updates its own table.
*   **Count-to-Infinity Problem:** A major drawback where bad news (link failure) travels slowly, causing loops.

### 3. Flooding
**Type:** Static/Simple Routing

Flooding is a simple routing technique where a packet received by a node is sent out to **all** other interfaces except the one it arrived on.

*   **Pros:** Highly robust; guarantees the packet reaches the destination if a path exists.
*   **Cons:** Generates massive traffic; requires a hop-count (TTL) to stop packets from circulating forever.

---

## Congestion Control Algorithms

Congestion control refers to techniques used to prevent too much data from being injected into the network, thereby avoiding network collapse.

### 1. Leaky Bucket Algorithm
**Purpose:** Traffic Shaping / Policing

Imagine a bucket with a small hole at the bottom. No matter how fast water enters the bucket, it leaks out at a constant rate.

*   **Input:** Data packets can arrive at variable rates (bursty traffic).
*   **Output:** Data flows out at a **constant, fixed rate**.
*   **Overflow:** If the bucket is full, incoming packets are discarded (dropped).
*   **Use Case:** Smooths out bursty traffic into a steady stream.

### 2. Token Bucket Algorithm
**Purpose:** Traffic Shaping (allows bursts)

The Token Bucket algorithm allows for some flexibility with bursty traffic, unlike the strict output rate of the Leaky Bucket.

*   **Mechanism:**
    *   Tokens are added to a bucket at a fixed rate.
    *   The bucket has a maximum capacity.
    *   To send a packet of size *n*, *n* tokens must be removed from the bucket.
    *   If there aren't enough tokens, the packet waits or is dropped.
*   **Bursts:** If the bucket is full of tokens, a sudden burst of data can be sent immediately (consuming the accumulated tokens).

---

## Comparison Summary

| Algorithm | Type | Key Feature |
| :--- | :--- | :--- |
| **Dijkstra** | Routing (Link State) | Global knowledge, efficient, no loops. |
| **Bellman-Ford** | Routing (Distance Vector) | Neighbor knowledge only, slower convergence. |
| **Leaky Bucket** | Congestion Control | Enforces constant output rate. |
| **Token Bucket** | Congestion Control | Allows defined data bursts. |
