# Windows Troubleshooting Notes

This file documents the main problems I ran into while setting up my active directory homelab and how I fixed them.

---

## 1. DNS / Domain Join Was Not Working
Problem: I realized I had a small typo in the IP address that DC was using, and it broke the entire thing. 

Fix: Correct typo in IP address.
- IP Address: 198.168.0.1 -> 192.168.0.1

---

## 2. Restoring Deleted Objects
Problem: I tried to simulate restoring an accidentally deleted account but couldn’t find the Deleted Objects container. Recycle Bin was not enabled.

Fix:
1. Confirmed domain functional level
2. Checked for deleted objects in PowerShell:
   Get-ADObject -filter 'isdeleted -eq $true' -includeDeletedObjects
3. Enabled recycle bin:
   Enable-ADOptionalFeature 'Recycle Bin Feature' -Scope ForestOrConfigurationSet -Target lab.com

---

## 3. Client1 Logon Kept Failing for Most Accounts
Problem: Logging into Client1 failed with the error: “We can’t sign you in with this credential because your domain isn’t available.” This happened when DC was not fully booted, and Client1 attempted to log in with an account that did not have cached credentials.

Fix: Ensure DC is fully booted before logging into Client1.

---

## 4. VM Freezing / Lagging Constantly
Problem: Both VMs were freezing because they were using too many host resources.

Fix:
1. Set both VMs to 2048 MB RAM (initially at 4GB and 2GB)
2. Set both to 1 CPU core (intially at 2 cores each)
3. Avoid running multiple VMs at full load at the same time

---

## 5. Client was not addressing to IPv4 properly
Problem: Client1's IPv4, when running ipconfig on CLI, used an APIPA address meaning it tried to reach the DHCP server and failed.

Fix: I ran ipconfig /release and /renew and it switched to IPv4 within DHCP scope.

---

## 6. Client's adapter was missing default gateway
Problem: When running ipconfig on CLI, Client1's adapter had no default gateway set. The domain controller was registering its NAT adapter IP (10.0.2.15) in DNS instead of the internal network IP (192.168.0.1). This caused clients to resolve the DC to the wrong address, breaking domain join, DNS lookups, and general AD communication.

Fix:
1. Opened the NAT adapter → IPv4 → Advanced → DNS tab → unchecked “Register this connection’s addresses in DNS”
2. Kept DNS registration enabled only on the Internal Network adapter (192.168.0.1)
3. Deleted the incorrect A records in DNS that pointed to 10.0.2.15
4. Ran:
   - ipconfig /flushdns
   - ipconfig /registerdns
To refresh and re-register the correct IP

--- 

## 7. Domain unavailable from Client sign-in
Problem: When attempting to log in as user within domain on Client1 VM, an error generated saying "We can't sign you in with this credential because your domain isn't available..."

Fix:
1. Checked DC to make sure DNS IP didn't switch again.
2. Logged into Client1 using account made during installation of VM.
3. Opened Command Prompt in Administrative mode and ran:
   - ipconfig (recieved an APIPA address for IPv4)
   - ipconfig /flushdns
   - ipconfig /registerdns
