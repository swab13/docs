---
title: Switching Microsoft 365 Report Data Privacy On and Off
parent: Microsoft 365
---

# Switching Microsoft 365 Report Data Privacy On and Off
{: .d-inline-block }

**09 June 2026**
{: .label .label-grey }

The Graph API has functionality to determine if the Report Data Privacy is either on or off, but it also has the capability to changing it.

Here is PowerShell functions for each using the MG Graph PowerShell module.

Determine if privacy is on or off

```
function Get-ReportPrivacySetting {
  $Uri = "https://graph.microsoft.com/beta/admin/reportSettings"
  $Data = Invoke-MgGraph -Method GET -Uri $Uri
  if ($Data) {
    return $($Data.displayConcealedNames)
  }

  return $null
}
```

Enable the report privacy setting

```
function Enable-ReportPrivacy {
  $Uri = "https://graph.microsoft.com/V1.0/admin/reportSettings"
  $Body = @{}
  $Body.Add("displayConcealedNames","true")
  Invoke-MgGraphRequest -Uri $Uri -Method Patch -Body $Body
}
```

Disable the report privacy setting

```
function Disable-ReportPrivacy {
  $Uri = "https://graph.microsoft.com/V1.0/admin/reportSettings"
  $Body = @{}
  $Body.Add("displayConcealedNames","false")
  Invoke-MgGraphRequest -Uri $Uri -Method Patch -Body $Body
}
```
