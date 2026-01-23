# Final Report

## Design and Simulation of a Fault-Tolerant Corporate Network for a Medical Institution

---

## Introduction

In the course of my graduation qualification work, I focused on the design, implementation, and simulation of a fault-tolerant corporate network for a medical institution, specifically the City Clinical Infectious Diseases Hospital No. 1.

I chose this topic because modern medical facilities critically depend on uninterrupted access to information systems, electronic medical records, laboratory databases, internal communication services, and external internet resources. Even short-term network failures in such environments can directly affect the quality of medical services and patient safety.

The main objective of my work was not only to design a theoretical network model but also to practically implement and test a fault-tolerant architecture using Cisco Packet Tracer. Special attention was given to redundancy, dynamic routing, gateway availability, service reliability, and basic security mechanisms.

---

## Practical Part: Network Design and Implementation

### Initial Requirements and Design Goals

Before starting the practical implementation, I defined a set of key technical requirements based on the specifics of a medical institution:

- Continuous network availability with minimal downtime  
- Elimination of single points of failure (SPOF)  
- Redundant network paths and default gateways  
- Stable operation of critical services such as DHCP, DNS, and email  
- Secure administrative access to network devices  
- Scalability and ease of future expansion  

These requirements formed the basis for all architectural and configuration decisions.

---

### Logical Network Architecture

The network was designed using a hierarchical model consisting of routing devices, access switches, servers, and end-user workstations.

To logically separate different departments and services, I implemented multiple VLANs. This approach improves security, simplifies management, and reduces unnecessary broadcast traffic.

For inter-VLAN and inter-network routing, I intentionally selected dynamic routing instead of static routes in order to increase flexibility and fault tolerance.

---

### Dynamic Routing Using OSPF

As the primary interior gateway protocol, I implemented **OSPF (Open Shortest Path First)**.

#### Configuration Steps:
1. Enabled OSPF on all core and distribution routers  
2. Assigned unique router IDs  
3. Advertised all internal networks into the OSPF process  
4. Used Area 0 as the backbone area  

#### Purpose:
OSPF dynamically exchanges topology information between routers and calculates the shortest paths using Dijkstra’s algorithm. In the event of a link or router failure, traffic is automatically rerouted without manual intervention, which is critical for medical networks.

---

### Gateway Redundancy with HSRP

To eliminate a single point of failure at the default gateway level, I implemented **HSRP (Hot Standby Router Protocol)**.

#### Configuration Steps:
- Created an HSRP group on two routers  
- Assigned a virtual IP address as the default gateway for hosts  
- Configured priority values to determine the active router  
- Enabled preemption  

#### Purpose:
If the active router fails, the standby router automatically takes over gateway functions. This transition is transparent to end devices and does not interrupt network connectivity.

---

### Switching Layer and Spanning Tree Protocol

Cisco Catalyst 2960 switches were used at the access layer. Since redundant physical links were implemented to increase reliability, **Spanning Tree Protocol (STP)** was enabled.

#### Purpose:
STP prevents Layer 2 loops by blocking redundant paths while keeping them available as backups. If the active link fails, STP restores connectivity automatically.

---

### Network Services Implementation

#### DHCP Service

A centralized DHCP server was configured to dynamically assign IP addresses.

**Functions:**
- Automatic IP address allocation  
- Distribution of default gateway and DNS parameters  
- Reduced configuration errors  

---

#### DNS Service

A DNS server was deployed to resolve domain names for internal services.

**Purpose:**
DNS simplifies access to network resources and is essential for normal operation of modern applications and services.

---

#### Email Services (SMTP / POP3)

SMTP and POP3 services were configured to simulate internal email communication.

**Purpose:**
Email is a critical communication tool within medical institutions for reports, notifications, and coordination.

---

### Network Address Translation (NAT)

NAT was implemented on the edge router to provide internet access for internal devices using private IP addresses.

**Purpose:**
- Enables external connectivity  
- Conserves public IP addresses  
- Provides basic network isolation  

---

### Security Measures

#### Access Control Lists (ACLs)

Extended ACLs were used to restrict administrative access to network devices.

**Purpose:**
Only authorized hosts were allowed to access routers via management protocols.

---

#### Secure Remote Access (SSH)

SSH was configured instead of Telnet for device management.

**Purpose:**
SSH encrypts authentication credentials and management traffic, significantly improving security.

---

### Fault Tolerance Testing

To verify the effectiveness of the designed architecture, several failure scenarios were simulated:

- Shutdown of primary router interfaces  
- Failure of the active HSRP router  
- Physical link disconnections  
- Service availability checks during failures  

**Results:**
In all scenarios, traffic was successfully rerouted, gateway failover occurred automatically, and critical services remained accessible.

---

## Conclusion

In this graduation qualification work, I designed and simulated a fault-tolerant corporate network for a medical institution using Cisco Packet Tracer.

The practical implementation confirmed that redundancy mechanisms, dynamic routing protocols, gateway failover technologies, and proper service placement significantly increase network reliability. The conducted tests demonstrated that the network can maintain stable operation even during failures of individual components.

This project allowed me to consolidate theoretical knowledge and gain hands-on experience in network design, configuration, and troubleshooting, which is directly applicable to real-world enterprise environments.
