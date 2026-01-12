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
