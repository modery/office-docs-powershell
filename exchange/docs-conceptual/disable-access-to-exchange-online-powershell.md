---
title: "Enable or disable access to Exchange Online PowerShell"
ms.author: chrisda
author: chrisda
manager: dansimp
ms.date:
ms.audience: Admin
audience: Admin
ms.topic: article
ms.service: exchange-powershell
ms.localizationpriority: medium
ms.assetid: f969816a-2607-4655-9d47-9e8767fb5633
search.appverid: MET150
description: "Admins can learn how to enable or disable access to Exchange Online PowerShell for users in their organization"
---

# Enable or disable access to Exchange Online PowerShell

Exchange Online PowerShell enables you to manage your Exchange Online organization from the command line. By default, all accounts you create in Microsoft 365 are allowed to use Exchange Online PowerShell. Administrators can use Exchange Online PowerShell to enable or disable a user's ability to connect to Exchange Online PowerShell. Note that access to Exchange Online PowerShell doesn't give users extra administrative powers in your organization. A user's capabilities in Exchange Online PowerShell are still defined by role based access control (RBAC) and the roles that are assigned to them.

## What do you need to know before you begin?

- Estimated time to complete each procedure: less than 5 minutes

- Microsoft 365 global admins have access to Exchange Online PowerShell, and can use the procedures in this article to configure Exchange Online PowerShell access for other users. For more information about permissions in Exchange Online, see [Feature Permissions in Exchange Online](/exchange/permissions-exo/feature-permissions).

- You can only use Exchange Online PowerShell to perform this procedure. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](connect-to-exchange-online-powershell.md).

- For detailed information about OPath filter syntax in Exchange Online, see [Additional OPATH syntax information](recipient-filters.md#additional-opath-syntax-information).

- You can also use Client Access Rules to block PowerShell access to Exchange Online. For details, see [Client Access Rules in Exchange Online](/Exchange/clients-and-mobile-in-exchange-online/client-access-rules/client-access-rules).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).

## Enable or disable access to Exchange Online PowerShell for a user

This example disables access to Exchange Online PowerShell for the user david@contoso.com.

```powershell
Set-User -Identity david@contoso.com -RemotePowerShellEnabled $false
```

This example enables access to Exchange Online PowerShell for the user david@contoso.com.

```powershell
Set-User -Identity david@contoso.com -RemotePowerShellEnabled $true
```

## Disable access to Exchange Online PowerShell for many users

To prevent access to Exchange Online PowerShell for a specific group of existing users, you have the following options:

- **Filter users based on an existing attribute**: This method assumes that the target user accounts all share a unique filterable attribute. Some attributes, such as Title, Department, address information, and telephone number, are visible only when you use the **Get-User** cmdlet. Other attributes, such as CustomAttribute1-15, are visible only when you use the **Get-Mailbox** cmdlet.

- **Use a list of specific users**: After you generate the list of specific users, you can use that list to disable their access to Exchange Online PowerShell.

### Filter users based on an existing attribute

To disable access to Exchange Online PowerShell for any number of users based on an existing attribute, use the following syntax:

```powershell
$<VariableName> = <Get-Mailbox | Get-User> -ResultSize unlimited -Filter <Filter>
```

```powershell
$<VariableName> | foreach {Set-User -Identity $_.WindowsEmailAddress -RemotePowerShellEnabled $false}
```

This example removes access to Exchange Online PowerShell for all users whose **Title** attribute contains the value "Sales Associate".

```powershell
$DSA = Get-User -ResultSize unlimited -Filter "(RecipientType -eq 'UserMailbox') -and (Title -like 'Sales Associate*')"
```

```powershell
$DSA | foreach {Set-User -Identity $_.WindowsEmailAddress -RemotePowerShellEnabled $false}
```

### Use a list of specific users

To disable access to Exchange Online PowerShell for a list of specific users, use the following syntax:

```powershell
$<VariableName> = Get-Content <text file>
```

```powershell
$<VariableName> | foreach {Set-User -Identity $_ -RemotePowerShellEnabled $false}
```

The following example uses the text file C:\My Documents\NoPowerShell.txt to identify the users by their accounts. The text file must contain one account on each line as follows:

> akol@contoso.com <br> tjohnston@contoso.com <br> kakers@contoso.com

After you populate the text file with the user accounts you want to update, run the following commands:

```powershell
$NPS = Get-Content "C:\My Documents\NoPowerShell.txt"
```

```powershell
$NPS | foreach {Set-User -Identity $_ -RemotePowerShellEnabled $false}
```

## View the Exchange Online PowerShell access for users

To view the Exchange Online PowerShell access status for a specific user, use the following syntax:

```powershell
Get-User -Identity <UserIdentity> | Format-List RemotePowerShellEnabled
```

This example displays the Exchange Online PowerShell access status of the user named Sarah Jones.

```powershell
Get-User -Identity "Sarah Jones" | Format-List RemotePowerShellEnabled
```

To display the Exchange Online PowerShell access status for all users, run the following command:

```powershell
Get-User -ResultSize unlimited | Format-Table -Auto Name,DisplayName,RemotePowerShellEnabled
```

To display only those users who don't have access to Exchange Online PowerShell, run the following command:

```powershell
Get-User -ResultSize unlimited -Filter 'RemotePowerShellEnabled -eq $false'
```

To display only those users who have access to Exchange Online PowerShell, run the following command:

```powershell
Get-User -ResultSize unlimited -Filter 'RemotePowerShellEnabled -eq $true'
```
