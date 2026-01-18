# Account Lockout Policy

This outlines the steps taken to create and configure an account lockout policy in Active Directory.

## Steps

1. Open Group Policy Management.
2. Right-click the domain name (lab.com).
3. Select “Create a GPO in this domain, and Link it here…”
4. Name the GPO: Account Lockout Policy
5. Right-click the Account Lockout Policy GPO -> Edit
6. In Group Policy Management Editor, go to:
   Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Lockout Policy
7. Configure the following settings:
   - Account lockout duration: 30 minutes
   - Account lockout threshold: 5 invalid logon attempts
   - Reset account lockout counter after: 30 minutes
8. Click Apply -> OK

## Applying the GPO

- In Group Policy Management, go to Group Policy Objects.
- Drag and drop the Account Lockout Policy GPO onto the LabComputers OU to apply it to the computers in that container.
