# Secure Multi-Site Enterprise Network

A secure multi-site enterprise network designed and simulated using **Cisco Packet Tracer**. The project demonstrates enterprise networking concepts including VLAN segmentation, inter-VLAN routing, centralized network services, access control, dynamic routing, secure device management, and Internet connectivity using NAT/PAT.

---

## Network Topology

![Enterprise Network Topology](network-topology.png)

The network consists of three major sections:

- **Headquarters Network** — HR, IT, Administration, and Server networks
- **Branch Office** — Remote LAN connected to headquarters
- **Simulated ISP Network** — Provides external network connectivity

---

## Network Architecture

### Headquarters

| VLAN | Department | Network | Gateway |
|---|---|---|---|
| 10 | Human Resources | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Information Technology | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Administration | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Server Network | 192.168.40.0/24 | 192.168.40.1 |

### Branch Office

| Network | Subnet | Gateway |
|---|---|---|
| Branch LAN | 192.168.50.0/24 | 192.168.50.1 |

### WAN / External Networks

| Connection | Network |
|---|---|
| R1-EDGE ↔ R2-ISP | 203.0.113.0/30 |
| R1-EDGE ↔ R3-BRANCH | 10.0.0.0/30 |
| Simulated Internet Network | 198.51.100.0/24 |

---

## Technologies Implemented

### VLAN Segmentation

Separate VLANs were created for HR, IT, Administration, and server infrastructure to logically segment departmental traffic.

### 802.1Q Trunking

Switch trunk links carry multiple VLANs across the headquarters switching infrastructure.

### Router-on-a-Stick

R1-EDGE uses 802.1Q subinterfaces to provide inter-VLAN routing between the headquarters VLANs.

### DHCP & DHCP Relay

A centralized DHCP server provides addressing to multiple VLANs.

`ip helper-address` is configured on router subinterfaces to forward DHCP requests to the centralized server.

### DNS

Internal DNS provides name resolution for:

`www.company.local`

which resolves to:

`192.168.40.10`

### Internal HTTP Portal

SERVER1 hosts an internal enterprise network operations portal accessible through the internal DNS name.

### Access Control Lists

Extended ACLs enforce traffic restrictions between departments while permitting required DNS and HTTP services.

Security policies include isolation of HR and Administration networks from unauthorized inter-department communication.

### SSH v2

Secure remote administration is configured on R1-EDGE using SSH version 2 and local authentication.

Telnet access is restricted.

### Switch Port Security

Access ports use:

- Maximum one MAC address
- Sticky MAC learning
- Restrict violation mode

This limits unauthorized devices from accessing protected switch ports.

### NAT/PAT

R1-EDGE performs Port Address Translation (PAT) for internal private networks.

Multiple internal devices share the external address:

`203.0.113.1`

when communicating with the simulated Internet network.

### OSPF Dynamic Routing

OSPF Area 0 provides dynamic routing between the headquarters and branch router.

Router IDs:

- R1-EDGE — `1.1.1.1`
- R3-BRANCH — `3.3.3.3`

The branch dynamically learns headquarters networks through OSPF.

---

## Network Services

The centralized server provides:

- DHCP
- DNS
- HTTP

Server configuration:

| Parameter | Value |
|---|---|
| Server | SERVER1 |
| IP Address | 192.168.40.10 |
| Network | VLAN 40 |
| Internal Domain | www.company.local |

---

## Security Features

The project implements multiple layers of network security:

- VLAN-based network segmentation
- Extended ACL traffic filtering
- Department isolation
- SSH v2 encrypted administration
- Telnet restriction
- Sticky MAC port security
- NAT/PAT address translation

---

## Testing & Verification

The network was tested for:

- DHCP address assignment
- Inter-VLAN routing
- DNS resolution
- HTTP connectivity
- ACL enforcement
- SSH remote login
- Port-security operation
- OSPF neighbor adjacency
- OSPF route learning
- Headquarters-to-branch connectivity
- NAT/PAT translation
- Branch-to-Internet connectivity

Example verification commands:

```text
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
show ip ospf neighbor
show access-lists
show ip nat translations
show ip nat statistics
show ip ssh
show port-security
```

---

## Project Files

### Packet Tracer Simulation

`Secure_Multisite_Enterprise_Network.pkt`

Open the file using **Cisco Packet Tracer** to inspect and run the complete network simulation.

### Topology

`network-topology.png`

Provides an overview of the complete enterprise network architecture.

---

## Key Learning Outcomes

This project provided hands-on experience with:

- Enterprise network design
- IPv4 subnetting and addressing
- VLAN configuration
- Cisco IOS CLI
- Inter-VLAN routing
- DHCP relay
- ACL design
- Network security
- NAT/PAT
- OSPF
- Network troubleshooting
- Multi-site network architecture

---

## Disclaimer

This project was created as an educational network simulation using Cisco Packet Tracer. The ISP and Internet infrastructure shown in the topology are simulated for demonstrating routing and NAT/PAT concepts.
