# Windows Active Directory Lab (VirtualBox)

This lab documents the setup and configuration of a Windows Server 2022 Active Directory Domain Services (AD DS) environment built using Oracle VirtualBox.

## Overview
- 1 Domain Controller (DC01)
- 1 Windows 10 Client (WS01)
- Host-Only private network
- Domain: lab.local

## Creating VM1 (Domain Controller) -> 
**Purpose:** AD DS, DNS Server, DHCP Server
- Name: DC01
- Iso Image: Windows Server 2022 (shows up as: SERVER_EVAL...)
- Unattended installation: unchecked -> NEXT
- RAM: 2048 MB
- CPU: 1 Core
- Disk 50 GB -> NEXT -> FINISH
- Right click DC01 Settings -> EXPERT -> Adapter 1: switch to "VirtualBox Host-Only Ethernet Adapter" -> OK
- Boot up: DC01 -> Choose language -> NEXT -> Click "Install Now" -> Choose "Windows Server 2022 Standard Evaluation (Desktop Experience)" -> NEXT -> Accept terms -> NEXT -> Custom -> Empty Drive -> NEXT
  
## Creating VM2 (Client Workstation) -> 
**Purpose:**Domain-joined PC for testing authentication, GPOs, shared folders, and user permissions.
- Name: WS01
- Iso Image: Windows.iso
- Same as DC01
- Boot up: WS01 -> Choose language -> NEXT -> Click "Install Now" -> Choose "Windows 10 Pro" -> NEXT -> Accept terms -> NEXT -> Custom -> Empty Drive -> NEXT

## Network Configuration

### DC01 (Static)
- IP Address: 192.168.56.10
- Subnet Mask: 255.255.255.0
- Default Gateway: 192.168.56.1
- DNS Server: 192.168.56.10

**DHCP Scope:**
- Start IP: 192.168.56.100
- End IP: 192.168.56.200
- Subnet Mask: 255.255.255.0

### WS01
**Obtained via DHCP:**
- IP Address: 192.168.56.100 (dynamic)
- DNS Server: 192.168.56.10
- DHCP Server: 192.168.56.10
- Primary DNS Suffix: lab.local

### VirtualBox Network Notes
- VirtualBox DHCP **disabled**
- Domain Controller responsible for DHCP/DNS

---

## Setup Steps (Summary)

### 1. Install Server Roles on DC01
- Active Directory Domain Services (AD DS)
- DNS Server
- DHCP Server

### 2. Promote DC01 to Domain Controller
- Created new forest: lab.local
- Server rebooted automatically after promotion

### 3. Configure DHCP
- Created scope: 192.168.56.100–200
- Activated and authorized the scope

### 4. Configure WS01 Network
- Set to obtain IP/DNS automatically
- Verified DHCP lease with:
  /release
  /renew
  /all
- Confirmed

### 5. Join WS01 to the Domain
- Open Settings -> System -> About -> Select “Rename this PC (Advanced)” -> Change... ->
- Enter domain: lab.local
- Enter domain admin credentials
- Restart WS01 and log in with: LAB\administrator

---

## Status
Active Directory environment successfully deployed.
DHCP and DNS functioning correctly.
Client joined and authenticated using AD credentials.
Group Policy Objects (GPOs) applied successfully.
Domain users can access resources based on permissions.
