### Useful Linux Commands.

#### Find files. 
* Find with non-root user
```
find / -type f -name user.txt 2> /dev/null 
```
* Find root suid files
```
find / -type f -user root -perm -u=s 2>/dev/null
```
* Find with root user
```
find / -type f -name root.txt 
```
