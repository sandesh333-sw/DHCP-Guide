# Packet Tracer Implementation Guide

## Network Topology Implementation Steps

### Step 1: Add Devices to the Workspace
1. Add three Cisco 2911 routers (one for each office: London, Manchester, and Leeds)
2. Add three Cisco 2960 switches (one for each office)
3. Add three wireless routers (one for each office)
4. Add servers (at least one per office)
5. Add end devices (PCs, laptops) - at least 2-3 per office

### Step 2: Connect Devices with Appropriate Cables

#### WAN Connections (Router to Router)
1. Connect London router to Manchester router using Serial DCE/DTE cables or Fiber connections
   - Use GigabitEthernet0/0 on London router
   - Use GigabitEthernet0/0 on Manchester router
2. Connect London router to Leeds router using Serial DCE/DTE cables or Fiber connections
   - Use GigabitEthernet0/1 on London router
   - Use GigabitEthernet0/0 on Leeds router
3. Connect Manchester router to Leeds router using Serial DCE/DTE cables or Fiber connections
   - Use GigabitEthernet0/1 on Manchester router
   - Use GigabitEthernet0/1 on Leeds router

#### LAN Connections (Within Each Office)
1. Connect each router to its local switch using Copper Straight-Through cables
   - Use GigabitEthernet0/2 on each router
   - Use GigabitEthernet0/1 on each switch
2. Connect each switch to its local server using Copper Straight-Through cables
3. Connect each switch to end devices (PCs, laptops) using Copper Straight-Through cables
4. Connect each switch to its wireless router using Copper Straight-Through cables

### Step 3: Configure WAN Interfaces with Public IP Addresses

#### London Router WAN Interfaces
1. Configure GigabitEthernet0/0 (to Manchester):
   - IP Address: 198.51.100.1
   - Subnet Mask: 255.255.255.252
2. Configure GigabitEthernet0/1 (to Leeds):
   - IP Address: 198.51.100.5
   - Subnet Mask: 255.255.255.252

#### Manchester Router WAN Interfaces
1. Configure GigabitEthernet0/0 (to London):
   - IP Address: 198.51.100.2
   - Subnet Mask: 255.255.255.252
2. Configure GigabitEthernet0/1 (to Leeds):
   - IP Address: 198.51.100.9
   - Subnet Mask: 255.255.255.252

#### Leeds Router WAN Interfaces
1. Configure GigabitEthernet0/0 (to London):
   - IP Address: 198.51.100.6
   - Subnet Mask: 255.255.255.252
2. Configure GigabitEthernet0/1 (to Manchester):
   - IP Address: 198.51.100.10
   - Subnet Mask: 255.255.255.252

### Step 4: Basic Router Configuration
For each router, configure:
1. Hostname (e.g., "London-Router", "Manchester-Router", "Leeds-Router")
2. Enable password
3. Console password
4. Telnet/VTY password
5. Banner message

### Step 5: Verify Physical Connectivity
1. Check that all devices are properly connected
2. Ensure no cable errors are shown in Packet Tracer
3. Verify that interfaces are up (no shutdown)


*Note: The IP addressing for LAN interfaces and VLAN configuration will be covered in Section 2 of the assignment.* 