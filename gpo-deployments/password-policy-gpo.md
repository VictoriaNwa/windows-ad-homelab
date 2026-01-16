# Password Policy

This outlines the steps taken to create and configure a domain-level password policy in Active Directory.

## Steps

1. Open Group Policy Management.
2. Right-click the domain name (lab.com).
3. Select “Create a GPO in this domain, and Link it here…”
4. Name the GPO: Password Policy
5. Right-click the Password Policy GPO -> Edit
6. In Group Policy Management Editor, go to:
   Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Password Policy

## Configuration

- Maximum password age: 90 days
- Minimum password age: 1 day 
- Minimum password length: 7 characters
- Password must meet complexity requirements: Enabled

## Applying the GPO

- In Group Policy Management, go to Group Policy Objects.
- Drag and drop the Password Policy GPO onto the LabComputers OU to apply it to the computers in that container.
