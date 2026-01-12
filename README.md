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

---

## Status
Active Directory environment successfully deployed.
DHCP and DNS functioning correctly.
Client joined and authenticated using AD credentials.
Group Policy Objects (GPOs) applied successfully.
Domain users can access resources based on permissions.
