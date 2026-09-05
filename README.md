# 🏢 Enterprise Campus Network Design

A complete **Cisco Packet Tracer** project simulating a multi-site enterprise network — a **Main Campus** with eight departmental VLANs and internal servers, connected over a **WAN link** to a **Branch Campus** with its own staff and student VLANs.

![Enterprise Campus Network Topology](Screenshot/Enterprise%20Campus%20Network.png)

---

## 📖 Overview

This project models a realistic enterprise network for an organization spanning two locations:

- **Main Campus** — houses eight department networks (Admin, HR, Finance, Business, Engineering & Computing, Arts & Design, Students Lab, IT Department), each on its own VLAN, plus centralized **Web** and **FTP** servers and an external **Cloud/Email Server** link.
- **Branch Campus** — a smaller remote site with **Staff** and **Student Lab** VLANs, connected back to the Main Campus over a **serial WAN link** through dedicated **2911 routers**.

The design demonstrates VLAN segmentation, inter-VLAN routing via a multilayer switch, hierarchical addressing, WAN connectivity between sites, and basic network services (Web, FTP, Email).

---

## 🗺️ Network Topology

```
                                    ┌───────────────────────┐
                                    │   Enterprise Campus    │
                                    │        Design          │
                                    └───────────────────────┘

  [Email Server] ── [2911 Cloud Router] ══WAN══ [2911 Main Campus Router]
   (20.0.0.0/30)         10.10.10.4/30                  │
                                                          │
                                          [3650-24PS Main Campus Switch]
                                                          │
        ┌─────────┬─────────┬─────────┬─────────┬────────┼────────┬─────────┐
      Admin      HR Team   Finance  Business    E&C     A&D   Students Lab  IT Dept
     VLAN 10    VLAN 20   VLAN 30   VLAN 40   VLAN 50  VLAN 60   VLAN 70   VLAN 80
                                                                          (Web + FTP Srv)

  [Main Campus Router] ══════════ WAN Link (10.10.10.0/30) ══════════ [Branch Campus Router]
                                                                                │
                                                             [3650-24PS Multilayer Switch2]
                                                                        │            │
                                                                     Staff       Student Lab
                                                                    VLAN 90        VLAN 100
```

---

## 🖥️ Devices Used

| Device Type              | Model         | Quantity | Role                                   |
|---------------------------|--------------|:--------:|-----------------------------------------|
| Router                    | Cisco 2911   | 3        | Main Campus, Branch Campus, Cloud/ISP  |
| Multilayer Switch         | Cisco 3650-24PS | 2     | Main Campus & Branch Campus core switch (inter-VLAN routing) |
| Access Switch             | Cisco 2960-24TT | 10    | Per-department / per-site access layer |
| PC                        | PC-PT        | 10       | End-user workstations                  |
| Printer                   | Printer-PT   | 9        | Departmental network printers          |
| Server                    | Server-PT    | 3        | Email Server, Web Server, FTP Server   |

---

## 🌐 IP Addressing Scheme

### Main Campus — Departmental VLANs

| Department               | VLAN ID | Subnet             |
|----------------------------|:-------:|---------------------|
| Admin                     | 10      | 192.168.1.0/24      |
| HR Team                   | 20      | 192.168.2.0/24      |
| Finance                   | 30      | 192.168.3.0/24      |
| Business                  | 40      | 192.168.4.0/24      |
| Engineering & Computing   | 50      | 192.168.5.0/24      |
| Arts & Design             | 60      | 192.168.6.0/24      |
| Students Lab (Main)       | 70      | 192.168.7.0/24      |
| IT Department (Web/FTP)   | 80      | 192.168.8.0/24      |

### Branch Campus — VLANs

| Department          | VLAN ID | Subnet             |
|-----------------------|:-------:|---------------------|
| Staff                 | 90      | 192.168.9.0/24      |
| Students Lab (Branch) | 100     | 192.168.10.0/24     |

### WAN / Transit Links

| Link                                   | Subnet            |
|------------------------------------------|--------------------|
| Cloud Router ↔ Main Campus Router        | 10.10.10.4/30      |
| Main Campus Router ↔ Branch Campus Router| 10.10.10.0/30      |
| Cloud (Email Server side)                | 20.0.0.0/30        |

---

## ✨ Key Features

- ✅ **VLAN Segmentation** — each department and site is isolated on its own VLAN for security and broadcast control.
- ✅ **Inter-VLAN Routing** — handled by 3650-24PS multilayer switches at both campuses.
- ✅ **Site-to-Site WAN Connectivity** — Main and Branch campuses linked via serial WAN interfaces on 2911 routers.
- ✅ **Centralized Services** — Web Server and FTP Server hosted in the IT Department VLAN; Email Server reachable via the Cloud/ISP router.
- ✅ **Scalable Hierarchical Design** — access, distribution (multilayer switch), and core/WAN layers clearly separated, following Cisco's hierarchical network model.
- ✅ **Structured IP Plan** — sequential /24 subnets per VLAN and dedicated /30 point-to-point links for WAN connections.

---

## 📂 Repository Structure

```
Enterprise-Campus-Network/
│
├── Enterprise Campus Networking Project.pkt   # Main Packet Tracer project file
├── Screenshot/
│   ├── Enterprise Campus Network.png          # Full topology (Main + Branch)
│   ├── Branch Campus Network.png              # Branch Campus close-up
│   └── Connected Network.png                  # Combined logical view
├── LICENSE
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) (version 8.x or later recommended)

### Running the Project
1. Clone or download this repository.
   ```bash
   git clone https://github.com/MUdevelops/Enterprise-Campus-Network-.git
   ```
2. Open **Cisco Packet Tracer**.
3. Load the `.pkt` file from the repository.
4. Switch to **Simulation Mode** to trace packets across VLANs and the WAN link, or use **Realtime Mode** to test connectivity (`ping`, `traceroute`) between devices.

### Suggested Tests
- `ping` between PCs in different VLANs on the same campus (verifies inter-VLAN routing).
- `ping` from a Main Campus PC to a Branch Campus PC (verifies WAN connectivity).
- Access the **Web Server** and **FTP Server** from client PCs.
- Send a test email via the **Email Server** on the Cloud segment.

---

## 🎯 Learning Objectives

This project was built to practice and demonstrate:
- VLAN creation and configuration on Cisco switches
- Inter-VLAN routing with a multilayer switch
- Static/default routing between campus sites over a WAN
- IP subnetting and addressing plan design
- Basic network services deployment (Web, FTP, Email)
- Reading and building logical network topologies in Packet Tracer

---

## 👤 Author

**MUdevelops**
Project designed and simulated in Cisco Packet Tracer.

---

## 📄 License

This project is licensed under the terms of the [LICENSE](LICENSE) file included in this repository.
