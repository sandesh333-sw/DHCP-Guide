# Beginner-Friendly Linux Server Setup Guide

This guide provides simplified instructions for setting up an Ubuntu Server with DHCP service, user management, and basic security measures.

## Part 1: Linux Server Installation

### Prerequisites
- VMware Workstation/Player/Fusion
- Ubuntu Server  LTS ISO
- 20GB free disk space
- 2GB RAM minimum

### Installation Steps
1. Create a new VM in VMware with "Typical" configuration
2. Select Ubuntu Server ISO file
3. Set VM name to "TechConsulting-Server"
4. Allocate 20GB disk space and 2GB RAM
5. Set Network Adapter to "Bridged" mode
6. Complete Ubuntu installation with default options
7. Create an admin user during installation
8. Install OpenSSH server when prompted
9. After installation, update the system:
   ```
   sudo apt update
   sudo apt upgrade -y
   ```

## Part 2: DHCP Server Configuration

### Install DHCP Server
```
sudo apt install -y isc-dhcp-server
```

### Configure Network Interface
```
sudo nano /etc/default/isc-dhcp-server
```

Set the interface:
```
INTERFACESv4="ens160"  # Use your actual interface name
INTERFACESv6=""
```

### Configure DHCP Server
```
sudo nano /etc/dhcp/dhcpd.conf
```

Add a basic configuration:
```
# Global parameters
default-lease-time 86400;          # 24 hours
max-lease-time 604800;             # 7 days
authoritative;

# DNS settings
option domain-name "techconsulting.local";
option domain-name-servers 8.8.8.8, 8.8.4.4;

# Main subnet declaration
subnet 172.16.35.0 netmask 255.255.255.0 {
  range 172.16.35.100 172.16.35.200;
  option routers 172.16.35.1;
  option broadcast-address 172.16.35.255;
}
```

### Start and Enable DHCP Server
```
sudo systemctl start isc-dhcp-server
sudo systemctl enable isc-dhcp-server
```

### Configure Firewall for DHCP
```
sudo ufw allow 67/udp
sudo ufw allow 68/udp
sudo ufw reload
```

## Part 3: User Management

### Create User Groups
```
# Create admin group
sudo groupadd admins

# Create IT staff group
sudo groupadd itstaff
```

### Create Administrative User
```
# Create admin user
sudo adduser admin1

# Add user to sudo and admin groups
sudo usermod -aG sudo,admins admin1
```

### Create Regular Staff User
```
# Create IT staff user
sudo adduser staff1

# Add user to IT staff group
sudo usermod -aG itstaff staff1
```

### Configure Sudo Access
```
sudo visudo
```

Add these lines:
```
# Allow members of admins group to execute any command
%admins ALL=(ALL:ALL) ALL

# Allow members of itstaff group to restart DHCP service
%itstaff ALL=(ALL) NOPASSWD: /bin/systemctl restart isc-dhcp-server, /bin/systemctl status isc-dhcp-server
```

## Part 4: Basic Security Measures

### Firewall Configuration
```
# Set default policies
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Allow SSH
sudo ufw allow ssh

# Enable the firewall
sudo ufw enable

# Check status
sudo ufw status
```

### SSH Hardening
```
sudo nano /etc/ssh/sshd_config
```

Make these basic changes:
```
# Disable root login
PermitRootLogin no

# Limit login attempts
MaxAuthTries 3

# Allow only specific groups
AllowGroups admins itstaff
```

Restart SSH:
```
sudo systemctl restart ssh
```

### Install Fail2ban for Brute Force Protection
```
sudo apt install -y fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

### Secure DHCP Configuration File
```
sudo chmod 640 /etc/dhcp/dhcpd.conf
```

## Verification Steps

### Check DHCP Server Status
```
sudo systemctl status isc-dhcp-server
sudo cat /var/lib/dhcp/dhcpd.leases
```

### Verify User Setup
```
# List all users
cat /etc/passwd

# List all groups
cat /etc/group

# Check group membership for a specific user
groups admin1
```

### Check Security Configuration
```
# Check firewall status
sudo ufw status verbose

# Check SSH configuration
sudo sshd -T | grep -E 'permitrootlogin|maxauthtries'

# Check fail2ban status
sudo fail2ban-client status
```

## Best Practices for a Secure Server

1. **Regular Updates**: Keep your system updated
2. **Strong Passwords**: Use strong passwords for all accounts
3. **Firewall**: Only allow necessary services
4. **Minimal Software**: Install only what you need
5. **Regular Backups**: Back up critical configuration files
6. **Monitoring**: Monitor logs for suspicious activity 