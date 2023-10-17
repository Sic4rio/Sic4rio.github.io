---
title: Active Directory Enumeration Using AD-Module 
date: 2023-10-11 14:30:00 +1100
categories: [hacking]
tags: [active-directory,windows,ad,enumeration,recon,clm]
---

![PowerShell Logo](https://www.techrepublic.com/wp-content/uploads/2020/09/powershell.jpg)


# Using ActiveDirectory Module for Domain Enumeration from PowerShell Constrained Language Mode

In this brief post, I'd like to share valuable insights gained from my Certified Red Team Professional (CRTP) training course, led by the instructor, Nikhil SamratAshok Mittal. During the course, I learned how to harness the power of Microsoft's PowerShell ActiveDirectory module, a skill that can prove indispensable for red teaming and penetration testing.

## The ActiveDirectory Module

The CRTP course introduced me to a fascinating technique that allows us to effectively use the ActiveDirectory module without the need for Remote Server Administration Tools (RSAT) or administrative privileges. This knowledge, shared by Nikhil Mittal during the training, provides red teamers with an essential tool in their arsenal.

Here's how you can make the most of the ActiveDirectory module:

1. **Obtain the Essential DLL**: If you have access to a server where the ActiveDirectory module is already installed (for instance, a Domain Controller), you can start by copying the `Microsoft.ActiveDirectory.Management.dll` file from `C:\Windows\Microsoft.NET\assembly\GAC_64\Microsoft.ActiveDirectory.Management` to your local machine.

   ```powershell
   PS C:\> Import-Module C:\ADModule\Microsoft.ActiveDirectory.Management.dll -Verbose
   ```


    Please note that running `Get-Command -Module ActiveDirectory` at this point will yield no results.

2. **Import the Module**: In order to fully harness the ActiveDirectory module's capabilities, import the module  from the server. Typically, you can find this directory nestled at `C:\Windows\System32\WindowsPowerShell\v1.0\Modules\ActiveDirectory/`. Now, import the module with these commands:

    ```powershell
    PS C:\> Import-Module C:\ADModule\Microsoft.ActiveDirectory.Management.dll -Verbose
    PS C:\> Import-Module C:\AD\Tools\ADModule\ActiveDirectory\ActiveDirectory.psd1
    PS C:\> Get-Command -Module ActiveDirectory
    ```

## A Memory-Efficient Update 

Thanks to a awesome Pull Request (PR) by @D1iv3, it's now possible to load the module from memory using `Import-ActiveDirectory.ps1`. This script brings a multitude of benefits, including minimal detection risks by antivirus (AV) software, an expansive array of cmdlets (cmdlet usage will breifly be explored in a this post), effective cmdlet filters, and the all-important endorsement from Microsoft.

For your convenience, Nikhil has shared a copy of the module from a Windows Server 2016 on [GitHub](https://github.com/samratashok/ADModule).

One of the most valuable perks of this technique is its  compatibility with PowerShell Constrained Language Mode (CLM) and low detection rate, making it an invaluable asset for restricted internal engagements.


# Microsoft.ActiveDirectory.Management.dll Cheat Sheet

## Domain Commands

- **Get-ADDomain**: Retrieve information about the current domain.
- **Set-ADDomain**: Modify properties of the current domain.
- **New-ADOrganizationalUnit**: Create a new Organizational Unit (OU) in the current domain.

## User and Group Commands

- **Get-ADUser**: Retrieve information about Active Directory users.
- **New-ADUser**: Create a new user in Active Directory.
- **Set-ADUser**: Modify properties of an Active Directory user.
- **Remove-ADUser**: Delete a user from Active Directory.
- **Get-ADGroup**: Retrieve information about Active Directory groups.
- **New-ADGroup**: Create a new group in Active Directory.
- **Add-ADGroupMember**: Add members to an Active Directory group.
- **Remove-ADGroupMember**: Remove members from an Active Directory group.

## Organizational Unit (OU) Commands

- **Get-ADOrganizationalUnit**: Retrieve information about Active Directory OUs.
- **New-ADOrganizationalUnit**: Create a new OU in Active Directory.
- **Set-ADOrganizationalUnit**: Modify properties of an OU.
- **Remove-ADOrganizationalUnit**: Delete an OU from Active Directory.

## Computer Commands

- **Get-ADComputer**: Retrieve information about Active Directory computers.
- **New-ADComputer**: Create a new computer account in Active Directory.
- **Set-ADComputer**: Modify properties of a computer account.
- **Remove-ADComputer**: Delete a computer account from Active Directory.

## Group Policy Commands

- **Get-GPInheritance**: View the inheritance of Group Policies.
- **Get-GPResultantSetOfPolicy**: Get the resultant set of policy for a user or computer.
- **New-GPO**: Create a new Group Policy Object (GPO).
- **Set-GPRegistryValue**: Configure registry-based policy settings.

## Query and Filter Commands

- **Get-ADObject**: Retrieve information about any object in Active Directory.
- **Search-ADAccount**: Search for user accounts that match specific criteria.
- **Search-ADGroup**: Search for groups that match specific criteria.
- **Search-ADUser**: Search for user accounts that match specific criteria.
- **Search-ADComputer**: Search for computer accounts that match specific criteria.

## Miscellaneous Commands

- **Get-ADForest**: Retrieve information about the Active Directory forest.
- **Get-ADSite**: Retrieve information about Active Directory sites.
- **Get-ADReplicationSite**: Retrieve information about replication sites.
- **Get-ADRootDSE**: Retrieve the root DSE of a domain controller.

Remember to replace placeholders with actual values and adapt the commands to your specific use case. This cheat sheet provides a starting point for managing Active Directory with the `Microsoft.ActiveDirectory.Management.dll` module.




## Special Thanks

A massive thank you to Nikhil SamratAshok Mittal the following resources and websites that taught me all of this:

- https://learn.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2022-ps
- https://github.com/samratashok/ADModule
- https://www.labofapenetrationtester.com/2018/10/domain-enumeration-from-PowerShell-CLM.html
- https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse/active-directory-enumeration-with-ad-module-without-rsat-or-admin-privileges
- https://notes.benheater.com/books/active-directory/page/powershell-ad-module-on-any-domain-host-as-any-user
- https://www.techrepublic.com/
