# Windows Troubleshooting Notes

This file documents the main problems I ran into while setting up my active directory homelab and how I fixed them.

---

## 1. DNS / Domain Join Was Not Working
**Problem:** I realized I had a small typo in the IP address that DC01 was using, but that was only part of the issue. I initially had two adapters enabled on DC01 (Host-Only + NAT). Mixing adapters caused DNS confusion, and the NAT adapter broke the domain join. Internet connectivity is a big no for domain controllers.

**Fix:** I rebuilt DC01 with only one adapter (Host-Only). Since I was still early in the setup, it wasn’t too much to redo.

Before rebuilding, I tried several steps that did **not** solve the root issue:  
1. Checked IP addresses  
2. Ran various network/terminal commands  
3. Disabled IPv6  
4. Turned off Windows Defender Firewall  

Looking back, simply disabling the NAT adapter in VirtualBox would have solved the problem without a rebuild.

---

## 2. RSAT Installation on WS01 for Active Directory Tools
**Problem:** WS01 was also configured with only a Host-Only adapter, which gave it no internet access. Because RSAT installs through Windows Update, it failed every time.

**Fix:** Temporarily added a NAT adapter for internet connectivity. Installed RSAT successfully. Removed the NAT adapter afterward.

---

## 3. Restoring Deleted Objects
**Problem:**  I tried to simulate restoring an accidentally deleted account but couldn’t find the Deleted Objects container in ADAC or ADUC. This turned out to be a common issue, upon my research, of Recycle Bin not being enabled.

**Fix:**  
1. Confirmed my domain functional level was already high enough  
2. Checked for deleted objects in PowerShell:  
   - Get-ADObject -filter 'isdeleted -eq $true' -includeDeletedObjects
3. Enabled recycle bin
   - Enable-ADOptionalFeature 'Recycle Bin Feature' -Scope ForestOrConfigurationSet -Target <root.domain>

---

## 4. WS01 Logon Kept Failing for Most Accounts
**Problem:** Everytime I tried to log onto WS01 with correct account credentials, WS01 showed the error: “We can’t sign you in with this credential because your domain isn’t available.” I was confused because that meant I needed my DC01 (domain controller) to be on to sign on on WS01 and I didn't typically need that carry out these functions before.

**Fix:** Ensure DC01 is fully booted before logging into WS01.

It worked before because WS01 was using cached credentials. When I tried logging in with an account that hadn’t logged in recently (no cached credentials), authentication failed because DC01 wasn’t available.

--- 

## 5. VM Freezing / Lagging Constantly
**Problem:** Both DC01 and WS01 kept freezing or lagging heavily. I originally allocated 4GB RAM + 2 CPU cores to DC01 and 2GB RAM + 2 cores to WS01, which pushed my laptop to its limit. VirtualBox was taking most of my host resources, causing everything to freeze.

**Fix:** Reduced resource allocation so my laptop could handle it:
1. Lowered RAM for both VMs to 2048 MB
2. Reduced CPU cores on both VMs to 1 core each
3. Also stopped running both simultaneously often.

After adjusting these values, the freezing stopped and performance stabilized for both the host and the VMs more regularly.
Once I did this, the freezing reduced and both machines performed more consistently without dragging down the host.

--- 

## 6. ADUC Error: “The server is not operational” When Trying to Open Active Directory Tools on WS01
**Problem:**  When I opened Active Directory Users and Computers (ADUC) on WS01, I received the error the above. This happened even though WS01 was already logged in and seemed to be connected to the domain. 

Once again, the root cause turned out to be the **two network adapters** issue. WS01 had two active at the same time:
- Adapter 1: Host-Only adapter (used for domain communication with DC01)
- Adapter 2: NAT adapter (which I'd recently added so WS01 could access Splunk via the Internet)

Because both adapters were active, Windows sometimes attempted to use the wrong network path (Adapter 2), which could not reach DC01 or its DNS services. I noticed this, after running command (ipconfig /all) on WS01 command line, to see where IPv4 addressed to and it was using an APIPA address (which is an address given when windows can't find the DHCP server). ADUC requires real-time access to the domain controller, so it failed instantly with “The server is not operational.”

**Fix:**  
Forced WS01 to use the Host-Only adapter for domain/DNS traffic by adjusting network configuration:
1. On WS01, opened Network Connections -> Change adapter options
2. On Adapter 1 (Host-Only):  
   - Set DNS server to the domain controller’s IP -> 192.168.56.10
3. On Adapter 2 (NAT):  
   - Removed or cleared DNS settings instead of fully disabling because of Splunk usage
4. Restarted WS01 to refresh routing and DNS
5. Opened ADUC again and the error was gone

AD tools now correctly route all domain traffic through the Host-Only adapter, while Splunk access can still use the NAT adapter when needed. 

However, I am considering installing Splunk onto my actual laptop and using forwarders on both DC01 and WS01 to avoid this issue altogether, and I think it would be more of a realistic setup anyways. Will update!
