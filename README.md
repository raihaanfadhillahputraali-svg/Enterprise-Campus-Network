# Enterprise Campus Network

## Overview

This project simulates a small enterprise campus network using Cisco IOSv and IOSvL2 devices in PNETLab.

The network is segmented into multiple VLANs representing different departments and uses a multilayer switch (MLS) for inter-VLAN routing. OSPF is implemented to provide dynamic routing between Layer 3 devices, while ACLs are used to enforce basic security policies between departments.

---

## Objectives

This project demonstrates the implementation of:

- VLAN Segmentation
- Access Ports
- 802.1Q Trunking
- Switch Virtual Interfaces (SVI)
- Inter-VLAN Routing
- OSPF Dynamic Routing
- Basic Access Control Lists (ACL)
- Enterprise Network Design

---

## Topology

![Topology](topology/topology.png)

> Replace this image after exporting your topology from PNETLab or Draw.io.

---

## Network Topology

```text
                 R1
                  |
            10.0.12.0/30
                  |
                 R2
                  |
            10.0.23.0/30
                  |
                MLS1
               /    \
              /      \
           SW1        SW2
          /   \      /   \
        PC1  PC2   PC3  PC4
```

---

## VLAN Design

| VLAN | Department | Network |
|------|------------|----------|
| 10 | IT | 192.168.10.0/24 |
| 20 | HR | 192.168.20.0/24 |
| 30 | Finance | 192.168.30.0/24 |
| 40 | Guest | 192.168.40.0/24 |

---

## Technologies Used

### Cisco IOSv
- OSPF
- Layer 3 Routing
- Static Routing

### Cisco IOSvL2
- VLAN
- Trunking
- SVI
- Inter-VLAN Routing

### PNETLab
- Network Emulation Platform

---

## IP Addressing

See:

```text
topology/ip-addressing.xlsx
```

---

## Configuration Files

| Device | Configuration |
|----------|----------|
| R1 | configs/R1.txt |
| R2 | configs/R2.txt |
| MLS1 | configs/MLS1.txt |
| SW1 | configs/SW1.txt |
| SW2 | configs/SW2.txt |

---

# Verification

## VLAN Verification

### Command

```bash
show vlan brief
```

### Result

![VLAN Verification](verification/vlan-brief.png)

**Screenshot Required**
- VLAN 10
- VLAN 20
- VLAN 30
- VLAN 40
- Assigned Ports

---

## Trunk Verification

### Command

```bash
show interfaces trunk
```

### Result

![Trunk Verification](verification/trunk-status.png)

**Screenshot Required**
- SW1 ↔ MLS1 trunk
- SW2 ↔ MLS1 trunk

---

## OSPF Neighbor Verification

### Command

```bash
show ip ospf neighbor
```

### Result

![OSPF Neighbor](verification/ospf-neighbor.png)

**Screenshot Required**
- R1 Neighbor
- R2 Neighbor
- FULL State

---

## Routing Table Verification

### Command

```bash
show ip route
```

### Result

![Routing Table](verification/routing-table.png)

**Screenshot Required**
- OSPF Routes
- Connected Routes
- VLAN Networks

---

## Connectivity Testing

### Successful Inter-VLAN Routing

```text
PC1 -> PC2
PC1 -> PC3
PC1 -> PC4
```

### Result

![Ping Tests](verification/ping-tests.png)

**Screenshot Required**
- Successful ping between departments

---

## ACL Verification

### Security Policy

Guest VLAN (40) is not allowed to access Finance VLAN (30).

### Allowed

```text
IT -> Finance
HR -> Finance
IT -> HR
```

### Denied

```text
Guest -> Finance
```

### Result

![ACL Verification](verification/acl-test.png)

**Screenshot Required**
- Successful ping from IT to Finance
- Failed ping from Guest to Finance

---

# Troubleshooting

## Issue 1 - Trunk Not Forming

### Problem

Traffic between VLANs was not crossing switches.

### Solution

Verified trunk interfaces using:

```bash
show interfaces trunk
```

Corrected switchport configuration.

---

## Issue 2 - OSPF Neighbor Down

### Problem

OSPF adjacency did not form.

### Solution

Verified:

```bash
show ip ospf neighbor
```

Checked:
- Interface status
- Network statements
- IP addressing

---

# Lessons Learned

Through this project I learned:

- VLAN segmentation and broadcast domain reduction
- Trunking using IEEE 802.1Q
- Inter-VLAN Routing with SVI
- OSPF Dynamic Routing
- ACL-based security controls
- Enterprise network troubleshooting
- Verification using Cisco IOS commands

---

# Future Improvements

Potential enhancements include:

- DHCP Server
- NAT
- GRE Tunnel
- HSRP
- EtherChannel
- IPv6
- Site-to-Site VPN
- Cisco + MikroTik Integration

---

# Conclusion

This project demonstrates the design and implementation of a small enterprise campus network using Cisco IOSv and IOSvL2 devices.

The implementation includes VLAN segmentation, trunking, inter-VLAN routing, OSPF dynamic routing, and ACL-based security controls commonly found in enterprise environments.

This project serves as a foundation for future enterprise networking projects and demonstrates practical skills relevant to Network Engineer, NOC Engineer, and Infrastructure Engineer roles.
