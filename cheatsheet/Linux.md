#### Useful Linux Commands.

* Find files. 
```
find / -type f -name user.txt 2> /dev/null (find with non-root user)
find / -type f -user root -perm -u=s 2>/dev/null (find root suid files)
find / -type f -name root.txt (find with root user)
```
