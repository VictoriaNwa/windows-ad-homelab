# Domain Controller (DC) Setup – VirtualBox

## 1. Create the Domain Controller VM
1. Open VirtualBox -> "New"
2. Name: DC
3. Select the ISO image that starts with:  SERVER_EVAL...
4. **Uncheck** Unattended Installation
5. Set:
   - Memory: 2048 MB
   - CPU: 1
   - Disk: *(leave default settings)*
6. Go to DC's Settings → Network
   - **Adapter 1:** NAT *(leave default)*
   - **Adapter 2:** "Enable" -> Internal Network

## 2. Installation
1. Boot DC -> Adjust language to your preference -> "Install now"
2. Choose -> Windows Server 2022 Standard Evaluation (Desktop Experience) This is for the GUI component, so its not just CLI.
3. "NEXT" -> Accept licensing terms -> "NEXT" -> Select "Custom" install to install hard drive from scratch -> NEXT -> Installation begins
4. Set password for administrator account -> Log in
5. Right click Start Menu -> "Network Connections" -> "Change adapter options" -> Right click an adapter -> "Status" -> "Details"
   - if IPv4 starts off 169.254.x.x it is APIPA (meaning its looking for DHCP and can not find it) = Internal Network
     - Rename "Internal Network"
     - Right click again -> "Properties" -> "Internet Protocol Version 4 (TCP/IPv4) **What I used...**
     - Use the following IP address: 192.168.0.1
     - Subnet mask : 255.255.255.0
     - No default gateway
     - Use the following DNS Server address: put the same as IP or 127.0.0.1 (124.0.0.1 addresses back to self, so both essentially do the same thing) -> OK
   - Name the other adapter, "Internet" and do nothing else
     - Internet adapter will get dynamic addressing through DHCP
6. Right click Start Menu -> "System" -> "Rename this pc" -> "DC"

---

## 3. Installing Active Directory on DC
1. Open Server Manager on DC -> "Add roles and features..." -> NEXT up until you must choose a server -> Choose "DC" -> NEXT -> Check "Active Directory Domain Services" -> "Add features" -> NEXT up until "Install -> Install
2. Once installed, on the top right in server manager, there will be a flag with a caution symbol, Click that -> "Promote this server to a domain controller" -> "Add a new forest" -> Root domain name: lab.com -> NEXT -> Create drsm password -> NEXT up until "Install" -> Install and computer will restart after.

---

## 4. Installing Remote Access Services and NAT on DC

1. Open Server Manager -> "Add roles and features..." -> NEXT up until you must choose a server -> Choose "DC" -> NEXT -> Check "Remote Access" -> NEXT up until "Role Services" -> Select "Routing" -> "Add features" -> NEXT up until "Install" -> Install
2. Server Manager -> "Tools" -> "Routing and Remote Access" -> Right click DC -> "Configure and enable ..." -> NEXT -> Choose "NAT" -> NEXT -> "Use this public interface to connect to the internet:" Select Internet -> NEXT -> FINISH

---

## 5. Installing DHCP and Setting up Scope

1. Open Server Manager -> "Add roles and features..." -> NEXT up until you must choose a server -> Choose "DC" -> NEXT -> Check "DHCP" -> "Add features" -> NEXT up until "Install" -> Install
2. Tools -> DHCP
3. Click the domain -> Right click IPv4, "New Scope" -> NEXT -> Name: 192.168.0.100-200 -> NEXT -> Start IP: 192.168.0.100 - End IP: 192.168.0.200 -> NEXT up until you get to "Router Default Gateway" page:
4. - 192.168.0.1 -> "Add" -> NEXT up until it asks about activating scope -> Yes -> Next -> Finish

Then, right click the server in DCHP -> "Authorize" -> "Refresh" (green checks should show on both IP's)
