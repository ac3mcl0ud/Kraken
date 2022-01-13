#### PowerView.ps1 Enumeration Guide


```
powershell -ep bypass

. .\PowerView.ps1

Get-NetDomain

Get-NetDomainController

Get-DomainPolicy

(Get-DomainPolicy)."system access"

Get-NetUser 	(select = grep in Linux)
		> Get-NetUser | select description
		> Get-NetUser | select samaccountname
		> Get-NetUser | select cn

Get-UserProperty
		> Get-UserProperty -Properties pwdlastset

Get-NetComputer (select = grep in Linux)
		> Get-NetComputer | select cn
		> Get-NetComputer | select operatingSystem		

Get-NetGroup

Get-NetGroup -GroupName *admin*

Invoke-ShareFinder

Get-NetGPO | select displayname, whenchanged			
```
