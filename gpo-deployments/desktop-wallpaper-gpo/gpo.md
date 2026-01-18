# Desktop Wallpaper

This outlines the steps taken to configure a desktop wallpaper using Group Policy in Active Directory.

## Steps

1. Enable Drag-and-Drop between the host machine and the VM:
   - Power off the Domain Controller VM.
   - In VirtualBox, open **Settings** for the DC VM.
   - Go to **General -> Features**.
   - Set **Drag-and-Drop** to **Bidirectional**.
   - (Optional) Set **Shared Clipboard** to **Bidirectional**.
   - Click OK and start the VM.

2. Create a wallpaper folder on the domain controller:
   - Open File Explorer on the DC.
   - Navigate to:
     C:\Windows\SYSVOL\sysvol\lab.com\scripts
   - Create a new folder named **Wallpapers**.

3. Transfer the wallpaper image from the host laptop to the VM:
   - On the host laptop, open File Explorer and locate the wallpaper image.
   - Drag the image directly into the following folder on the DC VM:
     C:\Windows\SYSVOL\sysvol\lab.com\scripts\Wallpapers
   - Example file: company-wallpaper.jpg

4. Note the UNC path to the image:
   \\lab.com\SYSVOL\lab.com\scripts\Wallpapers\company-wallpaper.jpg

5. Open Group Policy Management.
6. Right-click the domain name (lab.com).
7. Select “Create a GPO in this domain, and Link it here…”
8. Name the GPO: Desktop Wallpaper
9. Right-click the Desktop Wallpaper GPO -> Edit
10. In Group Policy Management Editor, go to:
    User Configuration -> Policies -> Administrative Templates -> Desktop -> Desktop
11. Open **Desktop Wallpaper**
12. Set the policy to **Enabled**
13. Configure the settings:
    - Wallpaper Name: \\lab.com\SYSVOL\lab.com\scripts\Wallpapers\company-wallpaper.jpg
    - Wallpaper Style: Fill
14. Click Apply -> OK

## Applying the GPO

- In Group Policy Management, go to Group Policy Objects.
- Drag and drop the Desktop Wallpaper GPO onto the LabUsers OU to apply it to users in that container.
