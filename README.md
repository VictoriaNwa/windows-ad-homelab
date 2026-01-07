# Windows Active Directory Lab (VirtualBox)

This lab documents the setup and configuration of a Windows Server 2022 Active Directory Domain Services (AD DS) environment built using Oracle VirtualBox.

## Overview
- 1 Domain Controller (DC01)
- 1 Windows 10 Client (WS01)
- Host-Only private network
- Domain: lab.local

## Network Configuration

### VM1 — DC01 (Domain Controller)
**Purpose:** AD DS, DNS Server, DHCP Server  
**IP Configuration (Static):**
- IP Address: 192.168.56.10
- Subnet Mask: 255.255.255.0
- Default Gateway: 192.168.56.1
- DNS Server: 192.168.56.10

**DHCP Scope:**
- Start IP: 192.168.56.100
- End IP: 192.168.56.200
- Subnet Mask: 255.255.255.0

### VM2 — WS01 (Client Workstation)
**Purpose:** Domain-joined PC for testing authentication and policies set in AD DS  
**Obtained via DHCP:**
- IP Address: 192.168.56.100 (dynamic)
- DNS Server: 192.168.56.10
- DHCP Server: 192.168.56.10
- Primary DNS Suffix: lab.local

### VirtualBox Network Notes
- Both VMs connected to the same **Host-Only Adapter**
- VirtualBox DHCP **disabled**
- Domain Controller responsible for DHCP/DNS

---

## 🛠️ Setup Steps (Summary)

### 1. Install Server Roles on DC01
- Active Directory Domain Services (AD DS)
- DNS Server
- DHCP Server

### 2. Promote DC01 to Domain Controller
- Created new forest: `lab.local`
- Server rebooted automatically after promotion

### 3. Configure DHCP
- Created scope: 192.168.56.100–200
- Set DHCP options (003, 006, 015)
- Activated and authorized the scope

### 4. Configure WS01 Network
- Set to obtain IP/DNS automatically
- Verified DHCP lease with:
  /release
  /renew
  /all
- Confirmed

### 5. Join WS01 to the Domain
- Open Settings > System > About > 
- Select “Rename this PC (Advanced)” > Change... >
- Enter domain: lab.local
- Enter domain admin credentials
- Restart WS01 and log in with: LAB\administrator

---

## Status
Active Directory environment successfully deployed.
DHCP and DNS functioning correctly.
Client joined and authenticated using AD credentials.

(Next steps to be added later: OU creation, users, GPOs)
