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
   
## 2. Installation
1. Boot DC -> Adjust language to your preference -> "Install now" -> "Don't have a product key"
2. Choose -> Windows 10 Pro -> NEXT -> Accept licensing terms -> NEXT -> Select "Custom" install to install hard drive from scratch -> NEXT -> Installation begins
3. NEXT to second keyboard layout -> SKIP -> "I don't have internet" -> "Continue with limited setup"
4. Name: user - Password: (skipped)
5. "Accept" and "Not now" for Cortana
6. Right click Start Menu -> "System" -> "Rename this pc (advanced)" -> "Change..." ->
   - Name: Client1
   - Activate domain
   - Domain Name: lab.com
   - REBOOT
