# Restrict Control Panel for Regular Staff

This outlines the steps taken to restrict access to the Control Panel and PC settings for regular staff users using Group Policy.

## Steps

1. Open Group Policy Management.
2. Right-click the domain name (lab.com).
3. Select “Create a GPO in this domain, and Link it here…”
4. Name the GPO: Restrict Control Panel
5. Right-click the Restrict Control Panel GPO -> Edit
6. In Group Policy Management Editor, go to:
   User Configuration -> Policies -> Administrative Templates -> Control Panel
7. Open **Prohibit access to Control Panel and PC settings**
8. Set the policy to **Enabled**
9. Click Apply -> OK

## Applying the GPO

1. In Group Policy Management, go to Group Policy Objects.
2. Drag and drop the Restrict Control Panel GPO onto the LabUsers OU.
3. Select the GPO and click OK.
4. Under **Security Filtering**, add:
   - Dept-Staff
   - Domain Computers
5. Go to **Delegation** -> Advanced and configure:
   - Dept-Staff = Read and Apply Group Policy
   - Domain Computers = Read only
6. Click Apply -> OK.
7. In **Security Filtering**, remove **Authenticated Users** and confirm.
