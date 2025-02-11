---
external help file: Microsoft.Rtc.Management.Hosted.dll-help.xml 
online version: https://docs.microsoft.com/powershell/module/skype/remove-cscallinglineidentity
applicable: Microsoft Teams, Skype for Business Online
title: Remove-CsCallingLineIdentity
schema: 2.0.0
manager: bulenteg
author: jenstrier
ms.author: jenstr
ms.reviewer:
---

# Remove-CsCallingLineIdentity

## SYNOPSIS
Use the `Remove-CsCallingLineIdentity` cmdlet to remove a Caller ID policy from your organization.

## SYNTAX

```
Remove-CsCallingLineIdentity [-Identity] <string> [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION
This cmdlet will remove a Caller ID policy from your organization or resets the Global policy instance to the default values.

## EXAMPLES

### -------------------------- Example 1 --------------------------
```
PS C:\> Remove-CsCallingLineIdentity -Identity Anonymous
```

This example removes a Caller ID policy.


## PARAMETERS

### -Identity
The Identity parameter identifies the Caller ID policy.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 
Applicable: Microsoft Teams, Skype for Business Online

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
The WhatIf switch causes the command to simulate its results. By using this switch, you can view what changes would occur without having to commit those changes.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi
Applicable: Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
The Confirm switch causes the command to pause processing, and requires confirmation to proceed.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf
Applicable: Microsoft Teams, Skype for Business Online

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS

[Get-CsCallingLineIdentity](Get-CsCallingLineIdentity.md)

[Grant-CsCallingLineIdentity](Grant-CsCallingLineIdentity.md)

[New-CsCallingLineIdentity](New-CsCallingLineIdentity.md) 

[Set-CsCallingLineIdentity](Set-CsCallingLineIdentity.md)
