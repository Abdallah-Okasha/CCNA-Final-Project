# Enterprise Multi-VLAN Routed Network Architecture

A complete, simulated enterprise network topology designed and configured in **Cisco Packet Tracer**. This project demonstrates scalable Layer 2 switching, Layer 3 inter-VLAN routing, dynamic OSPF routing across redundant router links, centralized IP addressing, and robust Layer 2/Layer 3 device security.

---

## Topology Overview

![Topology Diagram](./topology.png)

The infrastructure connects multiple functional departments and management zones across redundant routing paths:

* **Core & Distribution:** 3 Core Routers interconnected via point-to-point `/30` subnets (`192.168.100.0/30` through `192.168.140.0/30`), coupled with a Multilayer Switch (MLS1).
* **VLAN Segmentation:**
  * `VLAN 10, 20, 40, 50`: User access departments (`192.168.10.0/24`, `192.168.20.0/24`, `192.168.40.0/24`, `192.168.50.0/24`).
  * `VLAN 30`: Centralized Services / DHCP Server (`192.168.30.0/24`).
  * `VLAN 98` & `VLAN 99`: Dedicated Management subnets (`192.168.98.0/24`, `192.168.99.0/24`).

---

## Key Features & Configurations

### 1. Dynamic Routing & Link Redundancy
* **OSPF:** Configured across all core routers to ensure dynamic path selection, fast convergence, and automatic failover across redundant uplinks.
* **Point-to-Point Links:** Optimized subnet allocation using `/30` masks for inter-router transit links.

### 2. Layer 3 Inter-VLAN Routing
* Implemented Layer 3 routing via **Switch Virtual Interfaces (SVIs)** across both routers and the Multilayer Switch (MLS1), facilitating controlled traffic flow across subnets.
* Trunk links configured with 802.1Q encapsulation to carry multi-VLAN traffic across switches.

### 3. Centralized IP Management
* A centralized **DHCP Server** deployed in VLAN 30.
* Configured `ip helper-address` on Layer 3 gateways to forward DHCP broadcast requests across subnets to dynamically allocate IP addresses to all end-user endpoints.

### 4. Network Hardening & Security
* **Isolated Management VLANs:** VLAN 98 and VLAN 99 hosts are strictly designated for administrative access.
* **Encrypted Remote Management:** Direct **SSH** configuration for secure CLI access to all intermediate switches and routers.
* **Port Security:** Enforced on user-facing switch access ports (maximum 1 dynamic/sticky MAC address) to prevent unauthorized devices and MAC flooding attacks.
* **STP PortFast:** Enabled on all access ports for immediate transition to the forwarding state, bypassing standard Spanning Tree listening/learning delays.

---

## Tech Stack & Tools

* **Simulation Tool:** Cisco Packet Tracer
* **Protocols & Standards:** OSPF, 802.1Q (Trunking), Spanning Tree Protocol (STP / PortFast), DHCP, SSH, IPv4 (VLSM/Subnetting)
* **Devices Simulated:** Cisco 2911 Routers, Cisco Catalyst 3560 Multilayer Switch, Cisco Catalyst 2960 Switches, Generic End Devices & Servers

---
