# Drive Mapping

This outlines the steps taken to create and configure a drive mapping GPO in Active Directory.

## Steps

1. Create a folder to be shared:
   - File Explorer -> This PC -> Local Disk (C:) -> New -> Folder
   - Name the folder: LabShare
2. Right-click LabShare -> Properties -> Advanced Sharing
3. Check “Share this folder”
4. Click Permissions and configure:
   - Everyone = Read
   - Dept-Admins = Full Control
   - Dept-Helpdesk = Change, Read
   - Dept-Staff = Change, Read
5. Apply and close all windows.

Pay attention to the Network Path:
\\DC\LabShare

6. Open Group Policy Management.
7. Right-click the domain name (lab.com).
8. Select “Create a GPO in this domain, and Link it here…”
9. Name the GPO: Drive Mapping
10. Right-click the Drive Mapping GPO -> Edit
11. In Group Policy Management Editor, go to:
    User Configuration -> Preferences -> Windows Settings -> Drive Maps
12. Right-click -> New -> Mapped Drive
13. Configure the mapped drive:
    - Action: Update
    - Location: \\DC\LabShare
    - Drive Letter: A:
14. Click Apply -> OK

## Applying the GPO

- In Group Policy Management, go to Group Policy Objects.
- Drag and drop the Drive Mapping GPO onto the LabUsers OU to apply it to users in that container.
