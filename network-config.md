## Network Configuration

### DC (Static – Internal Network)
IP Address: 192.168.0.1  
Subnet Mask: 255.255.255.0  
Default Gateway: (leave blank)  
DNS Server: 192.168.0.1 or 127.0.0.1  
(DC can use either its own IP or loopback for DNS)

---

## DHCP Scope (Configured on DC)
Start IP: 192.168.0.100  
End IP: 192.168.0.200  
Subnet Mask: 255.255.255.0  
Default Gateway: 192.168.0.1  
DNS Server: 192.168.0.1  

---

### Client1 (Obtained via DHCP)
IP Address: 192.168.0.100 (Dynamic) 
Subnet Mask: 255.255.255.0  
Default Gateway: 192.168.0.1  
DNS Server: 192.168.0.1  
Primary DNS Suffix: lab.com  

---

## VirtualBox Network Notes
- Internal Network used for domain traffic
- NAT enabled on DC only
- VirtualBox DHCP disabled
- DC provides both DNS and DHCP
