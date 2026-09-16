Author: Pranay

Role: Tier 1 IT Support / Systems Administrator

Environment: Virtual Lab (VMware / VirtualBox)

Target Domain: corp.local

Host Identity: DC01

🎯 Objective
To perform a clean deployment of Windows Server 2022, configure static network properties, promote the server to an Active Directory Domain Controller (AD DS), and establish the primary DNS server for the corp.local domain.

🛠️ Step 1: Pre-Configuration & Static IP Assignment
Before installing Active Directory roles, a Domain Controller must have a fixed, static IP address to prevent network breakages caused by DHCP lease changes.

Opened Network Connections using Win + R > ncpa.cpl.

Opened the properties for the primary network interface (Ethernet0) and navigated to Internet Protocol Version 4 (TCP/IPv4).

Configured the following static network attributes:

IP Address: 192.168.1.10

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.1.1

Preferred DNS Server: 127.0.0.1 (Loopback address assigned because this server will host the primary DNS service for the domain).

Saved settings and verified connectivity via Command Prompt using ping 192.168.1.10.

🏷️ Step 2: System Hostname Standardization
To align with enterprise naming conventions, the default, randomly generated computer name was updated before domain promotion.

Launched Server Manager and selected Local Server.

Clicked the existing host name link to open System Properties.

Selected Change... and renamed the system to DC01.

Executed a system restart to commit the hostname change.

⚙️ Step 3: Installing Active Directory Domain Services (AD DS)
With static networking and identity established, the required binaries for Active Directory were deployed via Server Manager.

Opened Server Manager > selected Manage (top right) > clicked Add Roles and Features.

Followed the installation wizard defaults under Role-based or feature-based installation.

Under Server Roles, selected Active Directory Domain Services.

Accepted the prompt to include required management features (including ADUC and PowerShell tools).

Left all default selections on the Features screen and proceeded to click Install.

🚀 Step 4: Domain Controller Promotion & Forest Creation
Once the role binaries were installed, the server was promoted from a standalone server to the root Domain Controller of a new forest.

Selected the yellow notification flag in Server Manager and clicked Promote this server to a domain controller.

In the Deployment Configuration wizard, selected Add a new forest.

Specified the root domain name: corp.local.

Configured the Directory Services Restore Mode (DSRM) password and stored it securely.

Left default settings for DNS options and NetBIOS name (CORP).

Passed the prerequisite checks with no critical errors and initiated the installation.

Allowed the server to perform an automated reboot upon completion.

✅ Verification & Post-Deployment Checks
After rebooting, the following steps were taken to verify successful promotion:

Logon Verification: Authenticated as CORP\Administrator on the local console.

Role Verification: Opened Server Manager and verified that both AD DS and DNS services are running green with no critical service stops.

Administrative Tools Check: Confirmed access to Active Directory Administrative tools by opening Active Directory Users and Computers (dsa.msc).

DNS Health: Verified in DNS Manager (dnsmgmt.msc) that forward lookup zones for corp.local were populated automatically.
