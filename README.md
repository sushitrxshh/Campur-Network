# Campur-Network
This project simulates a campus network using Cisco Packet Tracer with a hierarchical design (Core, Distribution, Access). VLANs segment labs, classrooms, admin offices, and hostel areas for security and efficiency. Inter-VLAN routing via a multilayer switch enables controlled communication, creating a scalable and realistic campus network model.
<img width="4088" height="1729" alt="College Server" src="https://github.com/user-attachments/assets/50c5db21-0d82-4904-b338-5a50755d606e" />
### Download and install Cisco Packet Tracer using the link below to run this project file.

https://tinyurl.com/payeng076

# Key Features
- VLAN-based segmentation (VLAN 20–70)
- Inter-VLAN routing using a multilayer switch
- Trunk links between core and access switches
- Wired and wireless integration
- Centralized server connectivity
- Administrative and hostel isolation
# VLAN Structure
- VLAN 20 – CSE Lab 2
- VLAN 30 – CSE Lab 1
- VLAN 40 – Faculty Cabins
- VLAN 50 – Smart Classrooms
- VLAN 60 – Ground Floor (Library/Seminar Hall)
- VLAN 70 – Boys Hostel
# Devices Used
- Cisco ISR4331 Routers
- Multilayer Switch (Layer 3)
- Cisco 2960 Access Switches
- WRT300N Wireless Routers
- PCs and Network Printers
- Central Server
# Objectives
- Efficient traffic management
- Secure departmental isolation
- Scalable network design
- Real-world campus network simulation
## Technical Configuration Breakdown
### A. VLAN Configuration (On Access Switch)
```bash
enable
configure terminal
vlan 20
 name CSE_LAB2

vlan 30
 name CSE_LAB1

vlan 40
 name CABIN

vlan 50
 name SMART_CLASS

vlan 60
 name GROUND_FLOOR

vlan 70
 name HOSTEL

exit
```
### B. Assign Ports to VLAN
Example: Assigning ports for CSE Lab 2 (VLAN 20)
```bash
interface range fa0/1 - 12
switchport mode access
switchport access vlan 20
exit
```
Repeat for other VLANs using respective port ranges.
### C. Configure Trunk Port (Switch to Core)
```bash
interface fa0/24
switchport mode trunk
switchport trunk allowed vlan 20,30,40,50,60,70
exit
```
This allows VLAN traffic to pass between switches.
### D. Inter-VLAN Routing (Multilayer Switch)
Enable routing:
```bash
ip routing
```

Create SVI (Switch Virtual Interfaces):
```bash
interface vlan 20
ip address 192.168.20.1 255.255.255.0
no shutdown

interface vlan 30
ip address 192.168.30.1 255.255.255.0
no shutdown

interface vlan 40
ip address 192.168.40.1 255.255.255.0
no shutdown

interface vlan 50
ip address 192.168.50.1 255.255.255.0
no shutdown

interface vlan 60
ip address 192.168.60.1 255.255.255.0
no shutdown

interface vlan 70
ip address 192.168.70.1 255.255.255.0
no shutdown
```
Each VLAN now has a default gateway.
### E. PC Configuration

Example for VLAN 20 PC:

- IP Address: 192.168.20.10 

- Subnet Mask: 255.255.255.0 

- Default Gateway: 192.168.20.1

- Repeat according to VLAN subnet.

### F. Optional: DHCP Server Configuration

On multilayer switch:
```
ip dhcp pool VLAN20
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
dns-server 8.8.8.8
```

Repeat for other VLANs.

### G. Wireless Router Setup

- Connect WAN/LAN to switch

- Assign static IP in correct VLAN subnet

- Set SSID

- Enable WPA2 security
## Step-by-Step Configuration Guide (Packet Tracer)

### Step 1: Place Devices

Add 1 Multilayer Switch (Core)

- Add ISR4331 Routers

- Add 2960 Access Switches

- Add PCs and Printers

- Add WRT300N Wireless Routers

- Add Server

### Step 2: Connect Devices

- Use straight-through cables for PC → Switch

- Use trunk links between Switch → Core

- Connect routers to core switch

- Connect server to core

### Step 3: Create VLANs on Access Switches

- Go to CLI → configure VLANs.

Step 4: Assign Access Ports

- Assign correct VLAN to each lab/classroom block.

Step 5: Configure Trunk Ports

- Set trunk mode on ports connecting to core.

Step 6: Configure Multilayer Switch

- Enable ip routing

- Create VLAN interfaces

- Assign gateway IPs

### Step 7: Assign IP to PCs

- Manual or DHCP.

### Step 8: Test Connectivity

From PC:
```
ping 192.168.30.10
```

If inter-VLAN routing works, ping should succeed across departments.

### Step 9: Optional Security Upgrade

Add ACL example:
```
access-list 100 deny ip 192.168.70.0 0.0.0.255 192.168.20.0 0.0.0.255
access-list 100 permit ip any any

interface vlan 70
ip access-group 100 in
```

This blocks hostel from accessing lab network.



