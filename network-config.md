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
