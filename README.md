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

<img width="625" height="730" alt="image" src="https://github.com/user-attachments/assets/324f6295-8e5c-48f7-b794-1f7a705d0765" />


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

<img width="639" height="194" alt="image" src="https://github.com/user-attachments/assets/e551e2f5-de5e-4642-806a-ca404d45b65d" />


---

## Trunk Verification

### Command

```bash
show interfaces trunk
```

### Result

<img width="566" height="228" alt="image" src="https://github.com/user-attachments/assets/44b87a2c-1c0e-4047-baab-2019f0e2a2fb" />


---

## OSPF Neighbor Verification

### Command

```bash
show ip ospf neighbor
```

### Result

<img width="683" height="49" alt="image" src="https://github.com/user-attachments/assets/6b117718-1175-403a-a5d3-61b2ab9f20ed" />


---

## Routing Table Verification

### Command

```bash
show ip route
```

### Result

<img width="597" height="150" alt="image" src="https://github.com/user-attachments/assets/d6193e43-3380-459c-8748-59fb31fa7d77" />


---

## Connectivity Testing

### Successful Inter-VLAN Routing

```text
PC1 -> PC2
PC1 -> PC3
PC1 -> PC4
```

### Result

<img width="477" height="349" alt="image" src="https://github.com/user-attachments/assets/a2610e44-8dd6-4ef8-9157-b694a6aecff9" />


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

<img width="482" height="111" alt="image" src="https://github.com/user-attachments/assets/103471e1-6001-4bad-9ccf-ec65e7ff3497" />
<img width="488" height="109" alt="image" src="https://github.com/user-attachments/assets/974ebd44-d1ab-4adb-a8cb-72add7488010" />
<img width="480" height="113" alt="image" src="https://github.com/user-attachments/assets/154a7901-14b5-41e5-b03e-6f62fa6ba5ee" />
<img width="906" height="114" alt="image" src="https://github.com/user-attachments/assets/ecee7503-de73-4b2c-89fc-5fe5dc97fa65" />

---

## Troubleshooting

### Issue 1 - Unable to Configure Trunk Port

#### Problem

While configuring trunk links between switches, the command:

```bash
switchport mode trunk
```

returned an error and the interface would not enter trunk mode.

#### Investigation

Verified interface switchport settings and reviewed available trunk configuration options.

#### Root Cause

The switch was using trunk encapsulation mode `auto`, which prevented trunk mode from being enabled directly.

#### Resolution

Configured the trunk encapsulation type first:

```bash
switchport trunk encapsulation dot1q
switchport mode trunk
```

After applying the encapsulation, the interface successfully entered trunk mode.

#### Verification

```bash
show interfaces trunk
```

Confirmed that the interface was operating as an 802.1Q trunk and carrying VLAN traffic correctly.

#### Evidence

<img width="852" height="31" alt="image" src="https://github.com/user-attachments/assets/fe3aaca3-42f9-4693-b12e-5a3afa84ead1" />
<img width="330" height="30" alt="image" src="https://github.com/user-attachments/assets/8cbc1698-63ce-4a6e-8fc5-e9087c44ad31" />
<img width="562" height="195" alt="image" src="https://github.com/user-attachments/assets/5d69f6c4-e2e4-418c-8d06-b8f2693974fa" />

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
