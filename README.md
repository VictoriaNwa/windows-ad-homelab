# Windows Active Directory Lab (VirtualBox)

This lab documents the setup and configuration of a Windows Server 2022 Active Directory Domain Services (AD DS) environment built using Oracle VirtualBox.

## Overview
- 1 Domain Controller (DC)
- 1 Windows 10 Client (Client1)
- Hybrid (NAT + Internal Network)
- Domain: lab.com

## VM1 (Domain Controller) -> 
**Purpose:** AD DS, DNS Server, DHCP Server
- Name: DC
- Iso Image: Windows Server 2022 (shows up as: SERVER_EVAL...)
- Unattended installation: unchecked -> NEXT
- RAM: 2048 MB
- CPU: 1 Core
- Disk 50 GB -> NEXT -> FINISH
- Right click DC Settings -> EXPERT -> Adapter 1: NAT -> Adapter 2: Internal Network  OK
- Boot up: DC -> Choose language -> NEXT -> Click "Install Now" -> Choose "Windows Server 2022 Standard Evaluation (Desktop Experience)" -> NEXT -> Accept terms -> NEXT -> Custom -> Empty Drive -> NEXT
  
## VM2 (Client Workstation) -> 
**Purpose:**Domain-joined PC for testing authentication, GPOs, shared folders, and user permissions.
- Name: Client1
- Iso Image: Windows.iso
- Same as DC
- Boot up: Client1 -> Choose language -> NEXT -> Click "Install Now" -> Choose "Windows 10 Pro" -> NEXT -> Accept terms -> NEXT -> Custom -> Empty Drive -> NEXT

---

## Status
- Active Directory domain deployed and operational.  
- DNS and DHCP configured and verified on DC.  
- Client1 successfully joined to the domain and authenticating with domain accounts.  
- GPOs created, linked, and tested (shortcut deployment and security filtering).  
- NTFS permissions configured to enforce least-privilege access.  
- HelpDesk users can access authorized tools; Staff users restricted as expected.  

