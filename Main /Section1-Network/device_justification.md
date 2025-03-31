# Network Implementation and Device Justification

## Network Topology Overview

The network connects three office locations (London HQ, Manchester, and Leeds) of a technology consulting firm. Each location has:
- Router for WAN connectivity
- Switches for internal connectivity
- Wireless router for guest access
- End devices (computers and servers)

## Device Selection and Justification

### Routers
For each office, I've selected **Cisco 2911 Integrated Services Routers** for the following reasons:

1. **OSI Layer Functionality**: Operates at Layer 3 (Network Layer) for routing between different networks
2. **Hierarchical Layer**: Core layer device connecting different sites
3. **Performance Capability**: Provides up to 1 Gbps throughput suitable for a medium-sized business
4. **Security Features**: Includes firewall, VPN, and encryption capabilities
5. **Expansion Slots**: Supports modular expansion for future growth
6. **Dual WAN Support**: Each router needs at least 2 WAN interfaces for the full-mesh topology

### Switches
For each office, I've selected **Cisco Catalyst 2960-X Series Switches** for the following reasons:

1. **OSI Layer Functionality**: Primarily operates at Layer 2 (Data Link Layer) with some Layer 3 capabilities
2. **Hierarchical Layer**: Distribution and Access layer device
3. **VLAN Support**: Supports the creation of multiple VLANs for network segmentation
4. **PoE Capability**: Power over Ethernet for potential future IP phones or wireless APs
5. **Port Density**: 24 ports to accommodate multiple end devices
6. **Management**: Supports Cisco IOS with SNMP management

### Wireless Routers
For guest access in each office, I've selected **Cisco Aironet 1800 Series Access Points** for the following reasons:

1. **OSI Layer Functionality**: Primarily operates at Layers 1 and 2 (Physical and Data Link Layers)
2. **Hierarchical Layer**: Access layer device
3. **Security**: Supports WPA2/WPA3 Enterprise security
4. **VLAN Support**: Can create separate wireless networks mapped to different VLANs
5. **Dual-band Support**: Operates on both 2.4GHz and 5GHz frequencies

### Cabling Choices

1. **WAN Connections (Between Offices)**:
   - **Leased Line Fiber Optic**: Selected for high bandwidth, long distance capabilities, and security
   - Justification: Fiber optic provides higher bandwidth (10 Gbps+), better security (harder to tap), and immunity to electromagnetic interference compared to copper alternatives

2. **LAN Connections (Within Offices)**:
   - **Cat6a Ethernet Cable**: For switch-to-device connections
   - Justification: Supports up to 10 Gbps at distances up to 100 meters, future-proof for office environments
   - **Fiber Optic Backbone**: For router-to-switch connections
   - Justification: Higher bandwidth for backbone connections where traffic aggregates

## WAN Technology Justification

For this technology consulting firm, leased line fiber optic connections are chosen between offices for these reasons:

1. **High Bandwidth Needs**: As a technology consulting firm, large file transfers and potential cloud services require high bandwidth
2. **Reliability**: Dedicated leased lines provide guaranteed bandwidth without contention
3. **Security**: Private connections that don't traverse the public internet for sensitive data
4. **SLA Guarantees**: Service Level Agreements ensure uptime for critical business functions
5. **Latency**: Lower latency compared to alternatives like DSL or satellite

### Comparison with Alternative WAN Technologies:

| WAN Technology | Advantages | Disadvantages | Suitability |
|----------------|------------|---------------|-------------|
| Leased Line (Fiber) | High bandwidth, low latency, reliable, secure | Expensive, fixed locations | Highly suitable (selected) |
| DSL/Cable | Lower cost, widely available | Shared bandwidth, lower reliability | Not suitable for business-critical applications |
| MPLS | Traffic prioritization, VPN capabilities | Expensive, complex configuration | Good alternative but more complex than needed |
| 4G/5G | Mobility, quick deployment | Variable bandwidth, coverage issues | Suitable as backup only |
| Satellite | Available in remote areas | High latency, weather dependent | Not suitable for primary connection |

The technology consulting firm would prefer fiber-optic leased lines over DSL because client services and inter-office collaboration require guaranteed bandwidth, high security, and low latency that DSL cannot consistently provide. 