Role: Tier 1 IT Support / Systems Administrator

Environment: Windows 10/11 Pro (CLIENT01) & Windows Server 2022 (DC01.corp.local)

Subnet: 192.168.171.x

* Objective
To configure workstation networking properties, align endpoint DNS settings with the primary Domain Controller, resolve configuration errors, successfully join a Windows client machine (CLIENT01) to the corp.local domain, and verify domain authentication.

* Step-by-Step Implementation
1. Endpoint Networking & DNS Alignment
Joined endpoints must point directly to the Domain Controller’s DNS service to locate domain controllers and authentication endpoints.

Client Hostname: CLIENT01

IP Address: 192.168.171.150

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.171.2

Preferred DNS Server: 192.168.171.131 (Points directly to DC01)

2. Network & Name Resolution Verification
Ran network diagnostics in Command Prompt (cmd) on CLIENT01 to ensure connectivity and domain discovery before executing the join:

DOS
ping 192.168.171.131
nslookup corp.local
Result: Confirmed successful packet transmission and proper IP-to-domain mapping (corp.local -> 192.168.171.131).

3. Executing the Domain Join Operation
Opened System Properties on CLIENT01 (Win + R > sysdm.cpl).

Navigated to Computer Name > Change....

Changed member status from WORKGROUP to Domain: corp.local.

Authenticated the request using Domain Administrator credentials (CORP\Administrator).

Received the official confirmation pop-up: "Welcome to the corp.local domain."

Initiated a system restart to complete object registration in Active Directory.

4. Authentication Testing
Selected Other user on the CLIENT01 logon screen after reboot.
Logged in using CORP\Administrator credentials.
DOS
whoami
Output: corp\administrator

* Troubleshooting & Expected Failures
Reconciled Symptom / ErrorRoot CauseResolution ExecutedGateway Syntax Error Typo in gateway field (192.1688.171.2). Re-entered IPv4 properties in ncpa.cpl and corrected the octet to 192.168.171.2.Server: Unknown in nslookup. Lack of an IPv4 Reverse Lookup Zone (PTR record) on DC01.Identified as a non-blocking DNS artifact; forward lookup succeeded (192.168.171.131) and domain join proceeded without issues.Missing User Error: Attempted authentication using unprovisioned user accounts (e.g., jdoe).Switched to the active CORP\Administrator account to authorize the domain join.

* Final Results & Key Takeaways: Centralized Identity: CLIENT01 is now registered as an active computer object in corp. local.Policy Readiness: Endpoint is positioned to receive Group Policy Objects (GPOs), network drive mappings, and centralized user logins.Support Standard: Completed the end-to-end endpoint onboarding workflow expected of a 1st Line IT Support Specialist.
