# Always Wait for Network at Startup

This outlines the steps taken to configure a Group Policy setting that forces computers to wait for network connectivity before startup and logon.

## Steps

1. Open Group Policy Management.
2. Right-click the domain name (lab.com).
3. Select “Create a GPO in this domain, and Link it here…”
4. Name the GPO: Always Wait for Network at Startup
5. Right-click the Always Wait for Network at Startup GPO -> Edit
6. In Group Policy Management Editor, go to:
   Computer Configuration -> Policies -> Administrative Templates -> System -> Logon
7. Open **Always wait for the network at computer startup and logon**
8. Set the policy to **Enabled**
9. Click Apply -> OK

## Applying the GPO

- In Group Policy Management, go to Group Policy Objects.
- Drag and drop the Always Wait for Network at Startup GPO onto the LabComputers OU to apply it to the computers in that container.
