# PowerShell Commands – Unit 4 Cloud Security Assignment

## Project: Launch a Windows VM and Connect Using RDP

This document contains the PowerShell commands used to inspect the Windows Server, create a local user, enable Windows Firewall, and create a text file on an AWS EC2 Windows Server instance.

## 1. Check Windows Server System Information

Display the computer name, Windows edition, version, and system architecture.

```powershell
Get-ComputerInfo | Select-Object CsName, WindowsProductName, WindowsVersion, OsArchitecture
```

## 2. Check Hardware Information

Display the system manufacturer, model, RAM, and number of processors.

```powershell
Get-CimInstance Win32_ComputerSystem |
Select-Object Manufacturer, Model, TotalPhysicalMemory, NumberOfProcessors
```

## 3. Create a New Local User Account

Prompt for a password without displaying its characters, then create a local account named `LabUser`.

```powershell
$Password = Read-Host "Enter a strong password" -AsSecureString

New-LocalUser -Name "LabUser" `
  -Password $Password `
  -FullName "Cloud Security Lab User" `
  -Description "User created for Unit 4 cloud security assignment"
```

**Security note:** Use a unique, strong password. Never save the actual password in this file or upload it to GitHub.

## 4. Verify the User Account

Check whether the local user account was created successfully.

```powershell
Get-LocalUser -Name "LabUser"
```

### Optional: Allow the User to Sign In Through RDP

Run this only if the new user needs Remote Desktop access.

```powershell
Add-LocalGroupMember -Group "Remote Desktop Users" -Member "LabUser"
```

The user does not need administrator privileges for this assignment.

## 5. Enable Windows Firewall

Enable Windows Firewall for all three network profiles.

```powershell
Set-NetFirewallProfile -Profile Domain,Private,Public -Enabled True
```

## 6. Verify Windows Firewall Status

Display the status of each firewall profile.

```powershell
Get-NetFirewallProfile |
Select-Object Name, Enabled
```

**Expected result:** The Domain, Private, and Public profiles should display `True` under `Enabled`.

## 7. Create a Text File on the Desktop

Create a file named `CloudSecurityLab.txt`.

```powershell
New-Item -Path "$env:USERPROFILE\Desktop\CloudSecurityLab.txt" `
  -ItemType File -Force
```

## 8. Write Text into the File

Add a message to the file.

```powershell
Set-Content -Path "$env:USERPROFILE\Desktop\CloudSecurityLab.txt" `
  -Value "Windows Server deployed on AWS EC2 for Unit 4 Cloud Security."
```

## 9. Verify the Text File

Read the file's contents to confirm that it was created successfully.

```powershell
Get-Content "$env:USERPROFILE\Desktop\CloudSecurityLab.txt"
```

## 10. Verify the RDP Security Configuration in AWS

Configure this in the **AWS EC2 Console**, not in PowerShell:

| Setting | Required value |
|---|---|
| Security group | `Windows-RDP-SG` |
| Inbound rule | RDP |
| Protocol | TCP |
| Port | `3389` |
| Source | My IP (`your-public-IP/32`) |

Restrict access to your current public IP address. Do not expose RDP to `0.0.0.0/0`.

## 11. Connect to the Windows Server

On your Windows computer:

1. Press `Win + R`.
2. Enter `mstsc`.
3. Enter the EC2 instance's public IPv4 address.
4. Click **Connect**.
5. Enter the appropriate Windows username and password.

## 12. Security Best Practices

- Restrict RDP access to trusted IP addresses.
- Keep the EC2 private key secure.
- Use strong, unique passwords.
- Enable Windows Firewall.
- Avoid granting unnecessary administrator privileges.
- Never upload `.pem` files, passwords, AWS credentials, or other secrets to GitHub.
- Stop or terminate the EC2 instance when the practical is complete, as appropriate for your assignment and cost requirements.

## Conclusion

These commands demonstrate basic Windows Server administration on AWS EC2, including system inspection, local user management, firewall configuration, and file operations.
