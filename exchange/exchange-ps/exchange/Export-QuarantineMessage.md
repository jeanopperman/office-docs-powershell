---
external help file: Microsoft.Exchange.ServerStatus-Help.xml
online version: https://learn.microsoft.com/powershell/module/exchange/export-quarantinemessage
applicable: Exchange Online, Security & Compliance, Exchange Online Protection
title: Export-QuarantineMessage
schema: 2.0.0
author: chrisda
ms.author: chrisda
ms.reviewer:
---

# Export-QuarantineMessage

## SYNOPSIS
This cmdlet is available only in the cloud-based service.

Use the Export-QuarantineMessage cmdlet to export quarantined messages and files from your cloud-based organization. Messages are exported to .eml message files so you can open them in Outlook.

For files that were quarantined by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams, the files are exported in Base64 format.

For information about the parameter sets in the Syntax section below, see [Exchange cmdlet syntax](https://learn.microsoft.com/powershell/exchange/exchange-cmdlet-syntax).

## SYNTAX

### Identities
```
Export-QuarantineMessage -Identities <QuarantineMessageIdentity[]> [-Identity <QuarantineMessageIdentity>]
 [-CompressOutput]
 [-ForceConversionToMime]
 [-RecipientAddress <String>]
 [<CommonParameters>]
```

### IdentityOnly
```
Export-QuarantineMessage -Identity <QuarantineMessageIdentity>
 [-CompressOutput]
 [-ForceConversionToMime]
 [-RecipientAddress <String>]
 [<CommonParameters>]
```

## DESCRIPTION
You need to be assigned permissions before you can run this cmdlet. Although this topic lists all parameters for the cmdlet, you may not have access to some parameters if they're not included in the permissions assigned to you. To find the permissions required to run any cmdlet or parameter in your organization, see [Find the permissions required to run any Exchange cmdlet](https://learn.microsoft.com/powershell/exchange/find-exchange-cmdlet-permissions).

## EXAMPLES

### Example 1
```powershell
$e = Export-QuarantineMessage -Identity c14401cf-aa9a-465b-cfd5-08d0f0ca37c5\4c2ca98e-94ea-db3a-7eb8-3b63657d4db7
$e.BodyEncoding
$e | select -ExpandProperty Eml | Out-File "C:\My Documents\Export1_ascii.eml" -Encoding ascii
```

This example exports the quarantined message with the specified Identity value.

The first two commands determine the message encoding (the value of the BodyEncoding property in the output; for example, ascii).

The third command exports the message to the specified file using the message encoding that you found in the previous commands.

**Notes**:

- The `| select -ExpandProperty Eml`" part of the command specifies the whole message, including attachments.
- You need to use the Out-File cmdlet to write the .eml message file with the required encoding. If you use the default PowerShell redirection operator ">" to write the output file, the default encoding is Unicode, which might not match the actual message encoding.

### Example 2
```powershell
$e = Export-QuarantineMessage -Identity 9c6bb3e8-db9e-4823-9759-08d594179bd3\7fec89fe-41b0-ae67-4887-5bede017d111
$bytes = [Convert]::FromBase64String($e.eml)
[IO.File]::WriteAllBytes("C:\My Documents\Export1.txt", $bytes)
```

This example exports the quarantined file with the specified Identity value. The first command exports the file to a Base 64 string. The next two commands convert the string to byte format and write it to the output file.

## PARAMETERS

### -Identities
{{ Fill Identities Description }}

```yaml
Type: QuarantineMessageIdentity[]
Parameter Sets: Identities
Aliases:
Applicable: Exchange Online, Security & Compliance, Exchange Online Protection

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Identity
The Identity parameter specifies the quarantined message that you want to export. The value is a unique quarantined message identifier in the format `GUID1\GUID2` (for example `c14401cf-aa9a-465b-cfd5-08d0f0ca37c5\4c2ca98e-94ea-db3a-7eb8-3b63657d4db7`).

You can find the Identity value for a quarantined message by using the Get-QuarantineMessage cmdlet.

```yaml
Type: QuarantineMessageIdentity
Parameter Sets: Identities
Aliases:
Applicable: Exchange Online, Security & Compliance, Exchange Online Protection

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

```yaml
Type: QuarantineMessageIdentity
Parameter Sets: IdentityOnly
Aliases:
Applicable: Exchange Online, Security & Compliance, Exchange Online Protection

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -CompressOutput
{{ Fill CompressOutput Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:
Applicable: Security & Compliance

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ForceConversionToMime
{{ Fill ForceConversionToMime Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online, Security & Compliance

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -RecipientAddress
{{ Fill RecipientAddress Description }}

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online, Security & Compliance

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
