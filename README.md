# active-directory-lab
Windows Server 2019 Active Directory home lab built in VirtualBox with DHCP, DNS, and NAT configuration. Includes PowerShell scripts to automate creation and management of over 1,000 domain users. Designed to simulate an enterprise network environment for hands-on learning and sysadmin practice.
# 🧠 Active Directory Home Lab (VirtualBox + PowerShell)

## Overview
This lab demonstrates the setup of a **Windows Server 2019 Active Directory Domain Controller** in **Oracle VirtualBox**, configured with **DHCP**, **RAS/NAT**, and automated **user provisioning via PowerShell**.

## 🧩 Tools Used
- Oracle VirtualBox
- Windows Server 2019 ISO
- Windows 10 ISO
- PowerShell
- Active Directory Domain Services (AD DS)
- DHCP & NAT (Remote Access Service)

## 🧱 Lab Architecture
- **DC (Server19)** – Domain Controller, DHCP, NAT, DNS  
- **Client1 (Win10)** – Domain-joined workstation  
- **External NIC:** DHCP from home router (Internet access)  
- **Internal NIC:** 172.16.0.1/24 network for lab devices  

![Lab Diagram](docs/lab-diagram.png)

## ⚙️ Configuration Summary
- **Domain:** mydomain.com  
- **Internal Network:** 172.16.0.0/24  
- **DHCP Scope:** 172.16.0.100–200  
- **Gateway:** 172.16.0.1  
- **DNS:** 172.16.0.1  

## 💻 PowerShell Automation Example
```powershell
# create-1000-users.ps1
Import-Module ActiveDirectory
for ($i = 1; $i -le 1000; $i++) {
    $username = "LabUser$i"
    New-ADUser -Name $username `
               -SamAccountName $username `
               -UserPrincipalName "$username@mydomain.com" `
               -AccountPassword (ConvertTo-SecureString "P@ssword123" -AsPlainText -Force) `
               -Enabled $true
}
