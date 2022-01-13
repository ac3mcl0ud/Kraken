#### PowerView.ps1 Guide

   ```
  powershell -ep bypass

  . .\PowerView.ps1

  Get-NetDomain

  Get-NetDomainController

  Get-DomainPolicy

  (Get-DomainPolicy)."system access"

  Get-NetUser
      > Get-NetUser | select description
      > Get-NetUser | select samaccountname
      > Get-NetUser | select cn

    ```

