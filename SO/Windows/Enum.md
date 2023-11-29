---
tags:
  - Windows
  - SO
---
```powershell
powershell -ep bypass
Get-Content .ftp_client.ps1 | PowerShell.exe -noprofile -
. .\script1.ps1

powershell.exe -noprofile -executionpolicy bypass -file .\find.ps1

Get-ExecutionPolicy;
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Bypass -Force;
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted -Force;
```

# Grupos e Usuários
```powershell
whoami /all
whoami /priv
whoami /groups
```

## Get users e Get groups

```powershell
# get users
net user
net user <username>
wmic useraccount get name,sid

# para windows xp

net config Workstation | find "User name"
echo %username%

####################
# get groups

net localgroup administrators
Get-LocalGroupMember -Group "Administrators"
```

```powershell
```