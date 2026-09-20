# -Enterprise-Multi-Branch-Infrastructure-Redundant-Network-Architecture
This project demonstrates a multi-branch enterprise network designed in Cisco Packet Tracer.  The network connects a **Head Office in Lahore** with a **Branch Office in Islamabad** through an ISP network. The design includes network redundancy, VLAN segmentation, dynamic routing, DHCP, NAT/PAT, ACLs, and Site-to-Site IPsec VPN connectivity.

## Network Topology

### Head Office – Lahore

- PC-HR
- PC-IT
- Server-VLAN30
- SW-Access-HQ
- SW-Core1-HQ
- SW-Core2-HQ
- R1-HQ
- R2-HQ

### Branch Office – Islamabad

- PC-Branch
- SW-Islamabad
- R-Islamabad

### ISP

- R-ISP
- Internet simulation

## Main Technologies

- VLANs
- Inter-VLAN Routing
- Router-on-a-Stick
- HSRP High Availability
- OSPF Dynamic Routing
- LACP EtherChannel
- DHCP
- NAT/PAT
- NAT Exemption for VPN Traffic
- Extended ACLs
- Port Security
- SSH
- Site-to-Site IPsec VPN
- WAN Connectivity
- Network Troubleshooting

## VLAN Configuration

| VLAN | Name | Network |
|------|------|---------|
| 10 | HR | 192.168.10.0/24 |
| 20 | IT | 192.168.20.0/24 |
| 30 | Servers | 192.168.30.0/24 |
| 99 | Native | 192.168.99.0/24 |

## WAN Addressing

| Connection | Network |
|------------|---------|
| R1-HQ ↔ R-ISP | 200.1.1.0/30 |
| R-ISP ↔ R-Islamabad | 200.2.2.0/30 |
| Islamabad LAN | 192.168.40.0/24 |

## High Availability – HSRP

R1-HQ is configured as the primary HSRP router with:

- Priority: 110
- HSRP Active role
- Preempt enabled

R2-HQ is configured as the standby router with:

- Priority: 100
- HSRP Standby role
- Preempt enabled

If R1-HQ becomes unavailable, R2-HQ can take over the gateway role.

## OSPF

OSPF Area 0 is configured between R1-HQ and R2-HQ for internal HQ routing.

OSPF provides dynamic route exchange and supports the redundant HQ router design.

Verification:

```bash
show ip ospf neighbor
show ip route ospf
