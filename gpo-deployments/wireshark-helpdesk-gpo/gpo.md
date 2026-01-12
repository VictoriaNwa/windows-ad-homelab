# Deploying Wireshark to HelpDesk Using GPO + NTFS

This explains how I deployed Wireshark (downloaded on WS01) in my Active Directory homelab using Group Policy and NTFS permissions. The goal was to make Wireshark available to HelpDesk accounts only while blocking regular staff users. This setup reflects a realistic RBAC workflow.

---

## 1. Have a Helpdesk Security Group

Inside Active Directory Users and Computers:

- I already had a security group named dept-helpdesk (Global, Security)
- Three users were already in this group
- These users were also already inside the HelpDesk OU

---

## 2. Create and Link the GPO

Using Group Policy Management on DC01:

- Right-click the HelpDesk OU
- Select “Create a GPO in this domain, and Link it here…”
- Name the GPO: Deploy_Wireshark_Shortcut

---

## 3. Configure the Wireshark Shortcut

In the GPO editor, navigate to:
- User Configuration -> Preferences -> Window Settings -> Shortcuts

Create a new shortcut with the following values:

- Action: Create
- Name: Wireshark
- Target Path: C:\Program Files\Wireshark\Wireshark.exe (based on file path on WS01, since DC01 doesn't have Wireshark installed)
- Location: Desktop

This deploys a Wireshark icon to HelpDesk desktops.

---

## 4. Configure Security Filtering

In the GPO Scope tab:

- Leave Authenticated Users with Read permissions only (remove Apply GPO)
- Add HelpDesk_Group with Read + Apply
- Add Domain Computers with Read

This ensures the GPO only applies to HelpDesk users.

---

## 5. Restrict NTFS Permissions on Wireshark.exe

On WS01, where Wireshark is installed:

1. Right-click Wireshark.exe → Properties → Security → Advanced
2. Disable inheritance and choose “Convert...”
3. Remove:
   - Users
   - Domain Users
4. Add:
   - HelpDesk_Group → Read & Execute

This restricts execution so only HelpDesk can launch Wireshark.

---

## 6. Verification

### HelpDesk User
- Wireshark shortcut appears on desktop
- Wireshark launches normally

### Regular Staff User
- Shortcut appears (GPO delivered)
- Wireshark does not launch (blocked by NTFS permissions)

---

## Summary

This demonstrates:

- Deploying desktop shortcuts through Group Policy
- Applying NTFS restrictions to control application execution
- Enforcing least privilege and role-based access control
- Separating HelpDesk capabilities from regular staff accounts

Using GPO to distribute the shortcut and NTFS to enforce access, ensures only authorized users can run sensitive tools like Wireshark.
