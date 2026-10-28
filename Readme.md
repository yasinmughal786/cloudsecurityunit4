# Unit 4 – Cloud Security Assignment

## Launch a Windows VM and Connect Using RDP

### Overview
This project demonstrates how to launch a Windows Server virtual machine using Amazon EC2 and connect to it securely through Remote Desktop Protocol (RDP).

### Objectives
- Launch a Windows Server EC2 instance.
- Restrict RDP access to a specific public IP address.
- Connect to Windows Server using Remote Desktop.
- Inspect operating system and hardware information.
- Create a local user account with a strong password.
- Enable and verify Windows Firewall.
- Create and verify a text file on the server.

### Technologies Used
- Amazon Web Services (AWS)
- Amazon EC2
- Windows Server
- Remote Desktop Protocol (RDP)
- Windows PowerShell
- Windows Defender Firewall

### Security Configuration
| Setting | Configuration |
|---|---|
| Virtual machine | Windows Server on EC2 |
| Remote access | RDP |
| Protocol | TCP |
| Port | 3389 |
| Source | My public IP address only |
| Firewall | Enabled and verified |
| User management | Local user account |

### PowerShell Commands

Check system information:

```powershell
Get-ComputerInfo | Select-Object CsName, WindowsProductName, WindowsVersion, OsArchitecture
```

Verify the local user:

```powershell
Get-LocalUser -Name "LabUser"
```

Enable Windows Firewall:

```powershell
Set-NetFirewallProfile -Profile Domain,Private,Public -Enabled True
```

Verify firewall status:

```powershell
Get-NetFirewallProfile | Select-Object Name, Enabled
```

Create a text file:

```powershell
Set-Content -Path "$env:USERPROFILE\Desktop\CloudSecurityLab.txt" -Value "Windows Server deployed on AWS EC2 for Unit 4 Cloud Security."
```

### Screenshots
The `screenshots` folder contains evidence of the EC2 instance, RDP security group, Windows desktop, system information, user account, firewall status, and text file.

### Results
The results and screenshots will document the successful completion of each practical step. Only verified results should be reported.

### Conclusion
This practical demonstrates Windows Server deployment on AWS EC2, remote administration through RDP, user management, firewall configuration, and basic file operations.

### Security Note
Private key files, decrypted passwords, access credentials, and other secrets must never be uploaded to this repository.

### References
- [AWS EC2 Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
- [AWS RDP Connection Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-rdp.html)
