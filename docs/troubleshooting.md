IT Infrastructure Troubleshooting Lab Report

Case 1 — DHCP Issues

Problem: PC-CLIENT01 could not obtain an IP address automatically.

Investigation: Run `ipconfig /all` on client (got 169.254.x.x). Checked DHCP scope and service on SRV-DC01.

Root Cause: The DHCP Server service on SRV-DC01 was stopped.

Resolution: Started the DHCP Server service via `services.msc` and performed `ipconfig /renew` on the client.

Verification: PC-CLIENT01 successfully received IP `192.168.10.100` from the active scope.

Case 2 — DNS Resolution

Problem: Client cannot resolve the internal domain name 'corp.local'.

Investigation: Run `nslookup corp.local` failed, but `ping 192.168.10.10` was successful.

Root Cause: Static DNS IP address on the client's network adapter was misconfigured.

Resolution: Reconfigured the client's IPv4 properties to point to `192.168.10.10` as the Preferred DNS Server.

Verification: `nslookup corp.local` now successfully resolves to the domain controller's IP.

Case 3 — Domain Authentication

Problem: User 'nguyenvana' is unable to log into the domain corporate computer.

Investigation: Checked the user status inside Active Directory Users and Computers (ADUC) on SRV-DC01.

Root Cause: The user account was locked out due to multiple incorrect password attempts.

Resolution: Selected "Unlock account" in ADUC properties and applied changes.

Verification: User successfully logged in as `CORP\\nguyenvana`, confirmed via `whoami` command.

Case 4 — File Share Security

Problem: Unauthorized users can access restricted departmental folders.

Investigation: Checked NTFS security permissions on `C:\\CompanyShare\\IT`.

Root Cause: The 'Everyone' group had read access inherited on the folder.

Resolution: Removed 'Everyone', added `CORP\\IT-Group` with Modify permissions, and verified inherited flags.

Verification: 'nguyenvana' (IT) gained full access, while 'tranvanb' (Office) received "Access Denied".

Case 5 — Group Policy Objects

Problem: Corporate security baselines and wallpaper GPOs are not applying to PC-CLIENT01.

Investigation: Executed `gpresult /r` on client; the specific GPO was missing from the applied list.

Root Cause: The GPO was created but not linked to the correct Organizational Unit (OU) in Group Policy Management.

Resolution: Linked the GPO to the target OU and forced an immediate refresh using `gpupdate /force`.

Verification: Generated `gpresult /h C:\\gpresult.html` and confirmed the policy status is now "Enabled and Applied".
