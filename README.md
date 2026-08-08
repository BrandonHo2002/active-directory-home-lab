# Active Directory Home Lab

A hands-on Active Directory lab built using Windows Server 2022 and Windows 11 Pro in VMware Workstation Pro.

This project demonstrates the deployment and administration of a small Windows Active Directory environment, including user and group management, Organizational Units, DNS, domain joining, shared folders, and NTFS permissions.

## Lab Environment

- **Hypervisor:** VMware Workstation Pro
- **Domain Controller:** Windows Server 2022
- **Client:** Windows 11 Pro
- **Domain:** `mapletech.local`
- **Domain Controller:** `DC01`
- **Client Computer:** `CLIENT01`

## Project Objectives

The goal of this lab was to build a small Windows-based Active Directory environment and practice common IT administration tasks.

The lab objectives were to:

- Deploy Windows Server 2022 as a Domain Controller.
- Configure Active Directory Domain Services (AD DS) and DNS.
- Create the `mapletech.local` Active Directory domain.
- Organize users using Organizational Units (OUs).
- Create department-based security groups.
- Assign users to the appropriate security groups.
- Configure departmental shared folders.
- Apply NTFS permissions using security groups.
- Join a Windows 11 Pro workstation to the domain.
- Authenticate to the domain using an Active Directory user.
- Test and verify department-based file access.

## Active Directory Structure

The domain was organized using departmental Organizational Units:

```text
mapletech.local
├── Departments
│   ├── Executive
│   ├── Finance
│   ├── HR
│   ├── IT
│   ├── Marketing
│   └── Sales
│
└── Security Groups
    ├── Executive_Group
    ├── Finance_Group
    ├── HR_Group
    ├── IT_Group
    ├── Marketing_Group
    └── Sales_Group
