# Intune Registry Management

A PowerShell template for managing registry settings on Windows devices using **Microsoft Intune Remediations**.

## Features

- Runs as **SYSTEM** by design - manages both user and machine registry from one script, works in environments with strict **AppLocker** or **WDAC** policies, and avoids **Constrained Language Mode** restrictions
- Supports **HKCU** (all user profiles) and **HKLM**
- Works with **Microsoft Entra ID** and traditional AD joined devices
- All registry types: String, DWord, QWord, Binary, ExpandString, MultiString
- Three actions: **Set**, **Delete**, **DeleteKey**

## Usage

1. Download `Detect-Remediate-Registry-Template.ps1`
2. Modify the configuration section with your registry settings
3. Save two copies:
   - Detection: `$runRemediation = $false`
   - Remediation: `$runRemediation = $true`
4. Upload to **Intune** > **Devices** > **Scripts and remediations** > **Remediations**

## Configuration example

```powershell
$UserConfigs = @(
    @{
        Name        = "My Setting"
        Description = "What this does"
        BasePath    = "SOFTWARE\MyApp"
        Settings    = @(
            @{ Name = "SettingName"; Type = "String"; Value = "SettingValue" }
            @{ Action = "Delete"; Name = "UnwantedValue" }
            @{ Action = "DeleteKey"; Name = "OldSubKey" }
        )
    }
)
```

## Author

Martin Bengtsson - [imab.dk](https://www.imab.dk)
