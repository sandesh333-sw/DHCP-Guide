# VLAN and DHCP Configuration Guide

This guide provides step-by-step instructions for configuring VLANs and DHCP on the network devices in Packet Tracer.

## VLAN Configuration

### Step 1: Configure VLANs on Switches

#### London Switch Configuration:
```
Switch> enable
Switch# configure terminal
Switch(config)# hostname London-Switch
London-Switch(config)# vlan 10
London-Switch(config-vlan)# name Admin
London-Switch(config-vlan)# exit
London-Switch(config)# vlan 20
London-Switch(config-vlan)# name IT
London-Switch(config-vlan)# exit
London-Switch(config)# vlan 30
London-Switch(config-vlan)# name Guest
London-Switch(config-vlan)# exit
```

#### Manchester Switch Configuration:
```
Switch> enable
Switch# configure terminal
Switch(config)# hostname Manchester-Switch
Manchester-Switch(config)# vlan 10
Manchester-Switch(config-vlan)# name Admin
Manchester-Switch(config-vlan)# exit
Manchester-Switch(config)# vlan 20
Manchester-Switch(config-vlan)# name IT
Manchester-Switch(config-vlan)# exit
Manchester-Switch(config)# vlan 30
Manchester-Switch(config-vlan)# name Guest
Manchester-Switch(config-vlan)# exit
```

#### Leeds Switch Configuration:
```
Switch> enable
Switch# configure terminal
Switch(config)# hostname Leeds-Switch
Leeds-Switch(config)# vlan 10
Leeds-Switch(config-vlan)# name Admin
Leeds-Switch(config-vlan)# exit
Leeds-Switch(config)# vlan 20
Leeds-Switch(config-vlan)# name IT
Leeds-Switch(config-vlan)# exit
Leeds-Switch(config)# vlan 30
Leeds-Switch(config-vlan)# name Guest
Leeds-Switch(config-vlan)# exit
```

### Step 2: Assign Switch Ports to VLANs

For each switch, assign ports to the appropriate VLANs. Example for London Switch:

```
London-Switch(config)# interface range FastEthernet0/1-5
London-Switch(config-if-range)# switchport mode access
London-Switch(config-if-range)# switchport access vlan 10
London-Switch(config-if-range)# exit

London-Switch(config)# interface range FastEthernet0/6-10
London-Switch(config-if-range)# switchport mode access
London-Switch(config-if-range)# switchport access vlan 20
London-Switch(config-if-range)# exit

London-Switch(config)# interface range FastEthernet0/11-15
London-Switch(config-if-range)# switchport mode access
London-Switch(config-if-range)# switchport access vlan 30
London-Switch(config-if-range)# exit
```

Repeat similar configurations for Manchester and Leeds switches, adjusting port ranges as needed.

### Step 3: Configure Trunk Ports

Configure the port connecting to the router as a trunk port on each switch:

```
London-Switch(config)# interface GigabitEthernet0/1
London-Switch(config-if)# switchport mode trunk
London-Switch(config-if)# switchport trunk allowed vlan 10,20,30
London-Switch(config-if)# exit
```

Repeat for Manchester and Leeds switches.

## Router VLAN Interface Configuration

### Step 1: Configure Router Subinterfaces for VLANs

#### London Router:
```
Router> enable
Router# configure terminal
Router(config)# hostname London-Router

London-Router(config)# interface GigabitEthernet0/2
London-Router(config-if)# no shutdown
London-Router(config-if)# exit

London-Router(config)# interface GigabitEthernet0/2.10
London-Router(config-subif)# encapsulation dot1Q 10
London-Router(config-subif)# ip address 10.40.1.1 255.255.255.0
London-Router(config-subif)# exit

London-Router(config)# interface GigabitEthernet0/2.20
London-Router(config-subif)# encapsulation dot1Q 20
London-Router(config-subif)# ip address 10.40.2.1 255.255.255.0
London-Router(config-subif)# exit

London-Router(config)# interface GigabitEthernet0/2.30
London-Router(config-subif)# encapsulation dot1Q 30
London-Router(config-subif)# ip address 10.40.3.1 255.255.255.0
London-Router(config-subif)# exit
```

#### Manchester Router:
```
Router> enable
Router# configure terminal
Router(config)# hostname Manchester-Router

Manchester-Router(config)# interface GigabitEthernet0/2
Manchester-Router(config-if)# no shutdown
Manchester-Router(config-if)# exit

Manchester-Router(config)# interface GigabitEthernet0/2.10
Manchester-Router(config-subif)# encapsulation dot1Q 10
Manchester-Router(config-subif)# ip address 10.40.17.1 255.255.255.0
Manchester-Router(config-subif)# exit

Manchester-Router(config)# interface GigabitEthernet0/2.20
Manchester-Router(config-subif)# encapsulation dot1Q 20
Manchester-Router(config-subif)# ip address 10.40.18.1 255.255.255.0
Manchester-Router(config-subif)# exit

Manchester-Router(config)# interface GigabitEthernet0/2.30
Manchester-Router(config-subif)# encapsulation dot1Q 30
Manchester-Router(config-subif)# ip address 10.40.19.1 255.255.255.0
Manchester-Router(config-subif)# exit
```

#### Leeds Router:
```
Router> enable
Router# configure terminal
Router(config)# hostname Leeds-Router

Leeds-Router(config)# interface GigabitEthernet0/2
Leeds-Router(config-if)# no shutdown
Leeds-Router(config-if)# exit

Leeds-Router(config)# interface GigabitEthernet0/2.10
Leeds-Router(config-subif)# encapsulation dot1Q 10
Leeds-Router(config-subif)# ip address 10.40.33.1 255.255.255.0
Leeds-Router(config-subif)# exit

Leeds-Router(config)# interface GigabitEthernet0/2.20
Leeds-Router(config-subif)# encapsulation dot1Q 20
Leeds-Router(config-subif)# ip address 10.40.34.1 255.255.255.0
Leeds-Router(config-subif)# exit

Leeds-Router(config)# interface GigabitEthernet0/2.30
Leeds-Router(config-subif)# encapsulation dot1Q 30
Leeds-Router(config-subif)# ip address 10.40.35.1 255.255.255.0
Leeds-Router(config-subif)# exit
```

## DHCP Configuration

### Option 1: Configure DHCP on Routers

#### London Router DHCP Configuration:
```
London-Router(config)# ip dhcp excluded-address 10.40.1.1 10.40.1.49
London-Router(config)# ip dhcp excluded-address 10.40.1.201 10.40.1.254
London-Router(config)# ip dhcp excluded-address 10.40.2.1 10.40.2.49
London-Router(config)# ip dhcp excluded-address 10.40.2.201 10.40.2.254
London-Router(config)# ip dhcp excluded-address 10.40.3.1 10.40.3.49
London-Router(config)# ip dhcp excluded-address 10.40.3.201 10.40.3.254

London-Router(config)# ip dhcp pool ADMIN-VLAN
London-Router(dhcp-config)# network 10.40.1.0 255.255.255.0
London-Router(dhcp-config)# default-router 10.40.1.1
London-Router(dhcp-config)# dns-server 8.8.8.8
London-Router(dhcp-config)# lease 7
London-Router(dhcp-config)# exit

London-Router(config)# ip dhcp pool IT-VLAN
London-Router(dhcp-config)# network 10.40.2.0 255.255.255.0
London-Router(dhcp-config)# default-router 10.40.2.1
London-Router(dhcp-config)# dns-server 8.8.8.8
London-Router(dhcp-config)# lease 7
London-Router(dhcp-config)# exit

London-Router(config)# ip dhcp pool GUEST-VLAN
London-Router(dhcp-config)# network 10.40.3.0 255.255.255.0
London-Router(dhcp-config)# default-router 10.40.3.1
London-Router(dhcp-config)# dns-server 8.8.8.8
London-Router(dhcp-config)# lease 1
London-Router(dhcp-config)# exit
```

Repeat similar configurations for Manchester and Leeds routers, adjusting IP addresses according to the subnetting plan.

### Option 2: Configure DHCP on Servers

If using a server for DHCP (as in the Linux configuration section), configure the server with the following settings:

#### London DHCP Server:
- Server IP: 10.40.2.10
- Subnet Mask: 255.255.255.0
- Default Gateway: 10.40.2.1

DHCP Scopes:
1. Admin VLAN:
   - Network: 10.40.1.0/24
   - Range: 10.40.1.50 - 10.40.1.200
   - Default Gateway: 10.40.1.1
   - DNS Server: 8.8.8.8
   - Lease Time: 7 days

2. IT VLAN:
   - Network: 10.40.2.0/24
   - Range: 10.40.2.50 - 10.40.2.200
   - Default Gateway: 10.40.2.1
   - DNS Server: 8.8.8.8
   - Lease Time: 7 days

3. Guest VLAN:
   - Network: 10.40.3.0/24
   - Range: 10.40.3.50 - 10.40.3.200
   - Default Gateway: 10.40.3.1
   - DNS Server: 8.8.8.8
   - Lease Time: 1 day

Repeat similar configurations for Manchester and Leeds DHCP servers.

## Inter-VLAN Routing Configuration

Enable routing between VLANs on each router:

```
London-Router(config)# ip routing
Manchester-Router(config)# ip routing
Leeds-Router(config)# ip routing
```

## Verification Commands

Use these commands to verify your VLAN and DHCP configurations:

```
show vlan brief
show ip interface brief
show running-config
show ip dhcp binding
show ip dhcp pool
```
