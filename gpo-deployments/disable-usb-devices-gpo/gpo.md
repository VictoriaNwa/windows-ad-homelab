# Disable USB Devices

This outlines the steps taken to create and configure a GPO that blocks access to USB and other removable storage devices in Active Directory.

## Steps

1. Open Group Policy Management.
2. Right-click the domain name (lab.com).
3. Select “Create a GPO in this domain, and Link it here…”
4. Name the GPO: Disable USB Devices
5. Right-click the Disable USB Devices GPO -> Edit
6. In Group Policy Management Editor, go to:
   Computer Configuration -> Policies -> Administrative Templates -> System -> Removable Storage Access
7. Open **All Removable Storage classes: Deny all access**
8. Set the policy to **Enabled**
9. Click Apply -> OK

## Applying the GPO

- In Group Policy Management, go to Group Policy Objects.
- Drag and drop the Disable USB Devices GPO onto the LabComputers OU to apply it to the computers in that container.
