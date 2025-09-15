# Routing Information Protocol (RIP)

## Overview
**Routing Information Protocol (RIP)** is one of the oldest **distance-vector routing protocols** used in computer networks.  
It helps routers dynamically exchange routing information, allowing them to determine the best path for data packets within an **Autonomous System (AS)**.

RIP is widely used in small to medium-sized networks due to its simplicity and ease of configuration.

---

## Key Features
- **Type:** Distance-vector routing protocol
- **Algorithm:** Bellman-Ford
- **Maximum Hop Count:** 15 (16 is considered unreachable)
- **Updates Interval:** Every 30 seconds
- **Administrative Distance:** 120
- **Transport Protocol:** UDP (Port 520)

---

## Versions of RIP

| Version | Description |
|----------|-------------|
| **RIP v1** | Classful routing, does **not** support Variable Length Subnet Masking (VLSM). |
| **RIP v2** | Classless routing, supports VLSM and authentication. |
| **RIPng**  | RIP for IPv6 networks, supports IPv6 addressing. |

---

## How RIP Works
RIP routers periodically broadcast their **entire routing table** to neighboring routers.  
Each router:
1. **Receives routing updates** from its neighbors.
2. **Adds 1 to the hop count** for each learned route.
3. Updates its own routing table with the best path (lowest hop count).

> ⚠️ RIP uses **hop count as the only metric**, which makes it unsuitable for very large or complex networks.

---

## RIP Packet Types
RIP uses four main message types:

| Packet Type | Purpose |
|-------------|----------|
| **Request** | Asks neighboring routers to send an update. |
| **Response** | Contains routing information (updates). |
| **Update** | Periodic full routing table broadcast (every 30s). |
| **Triggered Update** | Immediate update when a topology change occurs. |

---

## RIP Configuration Example (Cisco CLI)
Below is an example of configuring RIP on a Cisco router:

```bash
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.1.0
Router(config-router)# network 192.168.2.0
Router(config-router)# no auto-summary
Router(config-router)# exit
Router(config)# end
Router# write memory
