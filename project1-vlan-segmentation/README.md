# Project 1 — VLAN Segmentation & Inter-VLAN Routing

## Overview
Configured VLAN segmentation and inter-VLAN routing across 
two Cisco Catalyst 2960X switches and a Cisco 2911 router 
using router-on-a-stick. Verified end-to-end connectivity 
between VLANs using physical end devices on real hardware.

## Hardware Used
- 2x Cisco Catalyst 2960X
- 1x Cisco 2911 Router
- 2x Laptops as end devices

## Network Topology
![Topology Diagram](project1-vlan-topology.png)

> Note: Raspberry Pi 4 is shown in the topology diagram 
> and will be configured in Project 3 for SNMP monitoring 
> and network visibility. Not configured in this project.

## VLAN Table
| VLAN | Name       | Subnet           |
|------|------------|------------------|
| 10   | Management | 192.168.10.0/24  |
| 20   | Staff      | 192.168.20.0/24  |
| 30   | Guest      | 192.168.30.0/24  |

## IP Addressing
| Device | Interface  | IP Address        |
|--------|------------|-------------------|
| R1     | Gi0/0.10   | 192.168.10.1/24   |
| R1     | Gi0/0.20   | 192.168.20.1/24   |
| R1     | Gi0/0.30   | 192.168.30.1/24   |
| SW1    | Vlan10     | 192.168.10.253/24 |
| SW2    | Vlan10     | 192.168.10.254/24 |

## Port Assignments

### SW1
| Port    | Mode   | VLAN |
|---------|--------|------|
| Gi1/0/1 | Trunk  | 10,20,30 |
| Gi1/0/2 | Access | VLAN 10 (Pi4 - Project 3) |
| Gi1/0/3 | Access | VLAN 20 |
| Gi1/0/4 | Access | VLAN 30 |

### SW2
| Port    | Mode   | VLAN |
|---------|--------|------|
| Gi1/0/1 | Trunk  | 10,20,30 |
| Gi1/0/2 | Trunk  | 10,20,30 (to R1) |
| Gi1/0/3 | Access | VLAN 20 |
| Gi1/0/4 | Access | VLAN 30 |

## Configuration Files
- [SW1 Config](sw1-config.txt)
- [SW2 Config](sw2-config.txt)
- [R1 Config](r1-config.txt)

## Verification Commands
```ios
show vlan brief
show interfaces trunk
show ip route
show ip interface brief
```

## Troubleshooting Encountered
1. SW1 management IP had a typo (192.18.10.253 instead of
   192.168.10.253) — identified using show interface vlan 10
   and corrected in configuration.
2. Laptop WiFi was active causing an IP conflict on the end
   device — disabled WiFi and retested with wired only.

## Results
- All VLANs active and verified on both switches
- Trunk links carrying VLANs 10, 20, 30 confirmed
- Inter-VLAN routing verified end to end
- Laptop on VLAN 20 (192.168.20.3) successfully pinged 
  laptop on VLAN 30 (192.168.30.3) through R1

## Video Demo
