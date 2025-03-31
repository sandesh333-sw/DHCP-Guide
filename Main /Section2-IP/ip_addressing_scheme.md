# IP Addressing and Subnetting Scheme

## Overview
This document outlines the IP addressing scheme for the technology consulting firm's network using the private IP range 10.40.0.0/16. The network is divided into subnets for each office location (London, Manchester, and Leeds) with further segmentation using VLANs for different departments.

## Subnetting Plan

The 10.40.0.0/16 network will be divided into three major subnets (one for each office) using a /20 subnet mask, providing 4,094 usable IP addresses per office:

| Office Location | Network Address | Subnet Mask | CIDR Notation | IP Range | Broadcast |
|----------------|-----------------|-------------|---------------|----------|-----------|
| London HQ | 10.40.0.0 | 255.255.240.0 | /20 | 10.40.0.1 - 10.40.15.254 | 10.40.15.255 |
| Manchester | 10.40.16.0 | 255.255.240.0 | /20 | 10.40.16.1 - 10.40.31.254 | 10.40.31.255 |
| Leeds | 10.40.32.0 | 255.255.240.0 | /20 | 10.40.32.1 - 10.40.47.254 | 10.40.47.255 |

## VLAN Configuration

Each office will have three VLANs to segment network traffic:

| VLAN ID | VLAN Name | Purpose |
|---------|-----------|---------|
| 10 | Admin | Administrative staff and management |
| 20 | IT | IT department staff and servers |
| 30 | Guest | Guest access for visitors and clients |

### VLAN Subnetting

Each VLAN within an office will be assigned a /24 subnet from the office's allocated range:

#### London Office VLANs:
| VLAN | Network Address | Subnet Mask | CIDR | IP Range | Broadcast |
|------|-----------------|-------------|------|----------|-----------|
| 10 (Admin) | 10.40.1.0 | 255.255.255.0 | /24 | 10.40.1.1 - 10.40.1.254 | 10.40.1.255 |
| 20 (IT) | 10.40.2.0 | 255.255.255.0 | /24 | 10.40.2.1 - 10.40.2.254 | 10.40.2.255 |
| 30 (Guest) | 10.40.3.0 | 255.255.255.0 | /24 | 10.40.3.1 - 10.40.3.254 | 10.40.3.255 |

#### Manchester Office VLANs:
| VLAN | Network Address | Subnet Mask | CIDR | IP Range | Broadcast |
|------|-----------------|-------------|------|----------|-----------|
| 10 (Admin) | 10.40.17.0 | 255.255.255.0 | /24 | 10.40.17.1 - 10.40.17.254 | 10.40.17.255 |
| 20 (IT) | 10.40.18.0 | 255.255.255.0 | /24 | 10.40.18.1 - 10.40.18.254 | 10.40.18.255 |
| 30 (Guest) | 10.40.19.0 | 255.255.255.0 | /24 | 10.40.19.1 - 10.40.19.254 | 10.40.19.255 |

#### Leeds Office VLANs:
| VLAN | Network Address | Subnet Mask | CIDR | IP Range | Broadcast |
|------|-----------------|-------------|------|----------|-----------|
| 10 (Admin) | 10.40.33.0 | 255.255.255.0 | /24 | 10.40.33.1 - 10.40.33.254 | 10.40.33.255 |
| 20 (IT) | 10.40.34.0 | 255.255.255.0 | /24 | 10.40.34.1 - 10.40.34.254 | 10.40.34.255 |
| 30 (Guest) | 10.40.35.0 | 255.255.255.0 | /24 | 10.40.35.1 - 10.40.35.254 | 10.40.35.255 |

## Router Interface IP Assignments

### London Router:
| Interface | IP Address | Subnet Mask | Purpose |
|-----------|------------|-------------|---------|
| GigabitEthernet0/0 | 198.51.100.1 | 255.255.255.252 | WAN link to Manchester |
| GigabitEthernet0/1 | 198.51.100.5 | 255.255.255.252 | WAN link to Leeds |
| GigabitEthernet0/2.10 | 10.40.1.1 | 255.255.255.0 | Admin VLAN Gateway |
| GigabitEthernet0/2.20 | 10.40.2.1 | 255.255.255.0 | IT VLAN Gateway |
| GigabitEthernet0/2.30 | 10.40.3.1 | 255.255.255.0 | Guest VLAN Gateway |

### Manchester Router:
| Interface | IP Address | Subnet Mask | Purpose |
|-----------|------------|-------------|---------|
| GigabitEthernet0/0 | 198.51.100.2 | 255.255.255.252 | WAN link to London |
| GigabitEthernet0/1 | 198.51.100.9 | 255.255.255.252 | WAN link to Leeds |
| GigabitEthernet0/2.10 | 10.40.17.1 | 255.255.255.0 | Admin VLAN Gateway |
| GigabitEthernet0/2.20 | 10.40.18.1 | 255.255.255.0 | IT VLAN Gateway |
| GigabitEthernet0/2.30 | 10.40.19.1 | 255.255.255.0 | Guest VLAN Gateway |

### Leeds Router:
| Interface | IP Address | Subnet Mask | Purpose |
|-----------|------------|-------------|---------|
| GigabitEthernet0/0 | 198.51.100.6 | 255.255.255.252 | WAN link to London |
| GigabitEthernet0/1 | 198.51.100.10 | 255.255.255.252 | WAN link to Manchester |
| GigabitEthernet0/2.10 | 10.40.33.1 | 255.255.255.0 | Admin VLAN Gateway |
| GigabitEthernet0/2.20 | 10.40.34.1 | 255.255.255.0 | IT VLAN Gateway |
| GigabitEthernet0/2.30 | 10.40.35.1 | 255.255.255.0 | Guest VLAN Gateway |

## Server IP Assignments

### London Servers:
| Server | IP Address | Subnet Mask | VLAN | Purpose |
|--------|------------|-------------|------|---------|
| DHCP Server | 10.40.2.10 | 255.255.255.0 | 20 (IT) | DHCP service for all VLANs |
| File Server | 10.40.2.11 | 255.255.255.0 | 20 (IT) | File storage and sharing |

### Manchester Servers:
| Server | IP Address | Subnet Mask | VLAN | Purpose |
|--------|------------|-------------|------|---------|
| DHCP Server | 10.40.18.10 | 255.255.255.0 | 20 (IT) | DHCP service for all VLANs |
| File Server | 10.40.18.11 | 255.255.255.0 | 20 (IT) | File storage and sharing |

### Leeds Servers:
| Server | IP Address | Subnet Mask | VLAN | Purpose |
|--------|------------|-------------|------|---------|
| DHCP Server | 10.40.34.10 | 255.255.255.0 | 20 (IT) | DHCP service for all VLANs |
| File Server | 10.40.34.11 | 255.255.255.0 | 20 (IT) | File storage and sharing |

## DHCP Scope Configuration

### London DHCP Server:
| VLAN | DHCP Scope | Default Gateway | DNS Server | Lease Time |
|------|------------|-----------------|------------|------------|
| 10 (Admin) | 10.40.1.50 - 10.40.1.200 | 10.40.1.1 | 8.8.8.8 | 7 days |
| 20 (IT) | 10.40.2.50 - 10.40.2.200 | 10.40.2.1 | 8.8.8.8 | 7 days |
| 30 (Guest) | 10.40.3.50 - 10.40.3.200 | 10.40.3.1 | 8.8.8.8 | 1 day |

### Manchester DHCP Server:
| VLAN | DHCP Scope | Default Gateway | DNS Server | Lease Time |
|------|------------|-----------------|------------|------------|
| 10 (Admin) | 10.40.17.50 - 10.40.17.200 | 10.40.17.1 | 8.8.8.8 | 7 days |
| 20 (IT) | 10.40.18.50 - 10.40.18.200 | 10.40.18.1 | 8.8.8.8 | 7 days |
| 30 (Guest) | 10.40.19.50 - 10.40.19.200 | 10.40.19.1 | 8.8.8.8 | 1 day |

### Leeds DHCP Server:
| VLAN | DHCP Scope | Default Gateway | DNS Server | Lease Time |
|------|------------|-----------------|------------|------------|
| 10 (Admin) | 10.40.33.50 - 10.40.33.200 | 10.40.33.1 | 8.8.8.8 | 7 days |
| 20 (IT) | 10.40.34.50 - 10.40.34.200 | 10.40.34.1 | 8.8.8.8 | 7 days |
| 30 (Guest) | 10.40.35.50 - 10.40.35.200 | 10.40.35.1 | 8.8.8.8 | 1 day |

## Reserved IP Ranges

Each VLAN has reserved IP ranges for static assignments:

- IP Range .1 - .49: Network infrastructure (routers, switches)
- IP Range .201 - .254: Static IP assignments for printers, servers, etc.
- IP Range .50 - .200: DHCP pool for dynamic assignment 