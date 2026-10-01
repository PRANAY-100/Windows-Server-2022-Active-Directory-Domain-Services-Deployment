# 🚀 Active Directory & Windows Enterprise Home Lab

## 📌 Project Overview
This repository documents the end-to-end design, deployment, and administration of a virtualized Windows Enterprise network environment. The primary objective is to simulate real-world Tier-1/Tier-2 IT Support, Identity & Access Management (IAM), and System Administration workflows using Windows Server 2022 and Windows 11 Enterprise workstations.

---

## 🛠️ Infrastructure Architecture & Specifications
* **Hypervisor:** Oracle VirtualBox / Microsoft Hyper-V
* **Domain Controller (DC):** Windows Server 2022 (`LAB-DC01` / Domain: `corp.local`)
* **Client Workstation:** Windows 11 Enterprise (`LAB-WIN11`, Domain-Joined)
* **IP Subnet:** `192.168.1.0/24`
* **Core Services:** Active Directory Domain Services (AD DS), DNS, DHCP, Group Policy (GPO), PowerShell

---

## 📁 Project Documentation & Lab Guides

* 📄 **[Lab 01: Windows Server 2022 & Active Directory Setup](./docs/01-Windows%20Server%202022%20%26%20Active%20Directory%20Setup.md)**
  * Configured static IPv4 networking, installed AD DS, and promoted server to Forest Root Domain Controller (`corp.local`).

* 📄 **[Lab 02: Domain-Join-Client Setup](./docs/02-Domain-Join-Client%20Setup.md)**
  * Binding client DNS to DC, testing name resolution, and joining Windows 11 Enterprise workstation to the domain.

* 📄 **[Lab 03: User Provisioning & Identity Management](./docs/03-User%20Provisioning,%20Identity%20Management.md)**
  * Built enterprise Organizational Unit (OU) structure (`Company Employees` $\rightarrow$ `HR`, `IT`, `Finance`, `Sales`).
  * Provisioned user accounts (`jdoe`), populated administrative metadata for GAL visibility, and enforced mandatory password resets on first logon.
  * Configured Role-Based Access Control (RBAC) global security groups and automated provisioning using PowerShell (`New-ADUser`).

* 📄 **[Lab 04: Support Ticket Workflows](./docs/04-Support%20Ticket%20Workflows.md)** *(In Progress)*
  * Simulating Tier-1 Help Desk ticket scenarios: Account Lockouts, Password Resets, Security Group memberships, and Shared Folder NTFS permissions.

---

## 🛠️ Key Technical Skills Demonstrated
* **Directory Services:** ADUC (`dsa.msc`), OU Hierarchy Design, User & Group Object Management, RBAC.
* **Security & Compliance:** Onboarding Security Policies, Account Lockout Mitigation, Principle of Least Privilege.
* **Network Infrastructure:** Static IP Binding, DNS Name Resolution, Domain Authentication, NTFS & SMB Share Permissions.
* **Automation:** Active Directory Administration via Windows PowerShell CLI.
