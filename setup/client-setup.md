# Client1 Setup – VirtualBox

## 1. Create the Client VM
1. Open VirtualBox -> "New" 
2. Name: Client1
3. ISO image: Windows.iso
4. **Uncheck** Proceed with Unattended Installation
5. Set:
   - Memory: 2048 MB
   - CPU: 1
   - Disk: *(leave default settings)*
7. Go to Client1's Settings → Network
   - **Adapter 1:** Internal Network
   - **Adapter 2:** NAT
   
## 2. Installation
1. Boot DC -> Adjust language to your preference -> "Install now" -> "Don't have a product key"
2. Choose -> Windows 10 Pro -> NEXT -> Accept licensing terms -> NEXT -> Select "Custom" install to install hard drive from scratch -> NEXT -> Installation begins
3. NEXT to second keyboard layout -> SKIP -> "I don't have internet" -> "Continue with limited setup"
4. Name: user - Password: (skipped)
5. "Accept" and "Not now" for Cortana
6. Right click Start Menu -> "Network Connections" -> Right click an adapter -> "Status" -> "Details"
   - if IPv4 says 169.254.x.x (APIPA Address)
     - that's the Internal Network
     - Rename: Internal Network
     - Properties -> Internet Protocol Version 4 (TCP\IPv4) -> "Use the following DNS server addresses:" -> Preferred DNS server: 192.168.0.1
   - the other adapter's IPv4 will most likely start with 10.x.x.x
     - that's the NAT
     - Rename: Internet
8. Right click Start Menu -> "System" -> "Rename this pc (advanced)" -> "Change..." ->
   - Name: Client1
   - Activate domain
   - Domain Name: lab.com
   - REBOOT
