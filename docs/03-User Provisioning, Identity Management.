Lab 03: Corporate OU Architecture & User Provisioning

Lab Objective
Configure Identity & Access Management (IAM) and Role-Based Access Control (RBAC) fundamentals on Windows Server 2022 using Active Directory Users and Computers (ADUC) and PowerShell. This lab simulates enterprise onboarding workflows, organizational structure design, and domain authentication verification from a Windows 11 client workstation.

Key Concepts & Technical Skills Covered
* Active Directory Domain Services (AD DS):** Directory hierarchy, OUs, User Objects, Global Security Groups.
* Identity Management:** User Principal Name (UPN), `sAMAccountName` standards, user attribute population for Global Address List (GAL) visibility.
* Security & Compliance:** Onboarding password force-reset on first logon, Principle of Least Privilege.
* CLI Automation:** Provisioning AD objects via Windows PowerShell (`New-ADUser`, `New-ADOrganizationalUnit`).

Step-by-Step Execution

1. Enterprise Organizational Unit (OU) Hierarchy
Built a scalable OU tree in ADUC (`dsa.msc`) to separate users, departments, and administrative boundaries:
* Created top-level OU: `Company Employees`
* Created child OUs for departmental segmentation:
  * `HR`
  * `IT`
  * `Finance`
  * `Sales`

2. User Account Provisioning & Identity Mapping
Provisioned a test employee account in the `HR` OU using standardized corporate attributes:
* Full Name:** Jane Doe
* User Logon Name (sAMAccountName): `jdoe`
* User Principal Name (UPN):`jdoe@lab.local`
* Account Flag: Enabled `User must change password at next logon` (`pwdLastSet = 0`)
* Metadata Populated: Job Title, Department, Office, and Manager attributes for directory searchability.

3. Client Verification & First Sign-In
1. Booted the domain-joined Windows 11 workstation (`LAB-WIN11`).
2. Initiated sign-in using domain credentials (`lab\jdoe`).
3. Verified the system enforced a mandatory password update before desktop session initialization.
4. Confirmed local user profile creation and verified active domain context via CLI (`whoami /all`).

#PowerShell Automation (CLI Execution)

In addition to the GUI workflow, the directory structure and user onboarding were executed using PowerShell commands run with elevated privileges on the Domain Controller:

powershell
# 1. Create Top-Level & Child OUs
New-ADOrganizationalUnit -Name "Company Employees" -Path "DC=lab,DC=local" -ProtectedFromAccidentalDeletion $true
New-ADOrganizationalUnit -Name "HR" -Path "OU=Company Employees,DC=lab,DC=local" -ProtectedFromAccidentalDeletion $true

# 2. Provision User Account with Temporary Password & Mandatory Reset
$Password = ConvertTo-SecureString "Welcome123!" -AsPlainText -Force

New-ADUser -Name "Jane Doe" `
           -GivenName "Jane" `
           -Surname "Doe" `
           -SamAccountName "jdoe" `
           -UserPrincipalName "jdoe@lab.local" `
           -Path "OU=HR,OU=Company Employees,DC=lab,DC=local" `
           -AccountPassword $Password `
           -ChangePasswordAtLogon $true `
           -Enabled $true `
           -Title "HR Specialist" `
           -Department "Human Resources"

# 3. Verify User Object Creation
Get-ADUser -Identity "jdoe" -Properties Title, Department, PasswordLastSet
Get-ADUser -Identity "jdoe" -Properties Title, Department, PasswordLastSet
