

#### Network File System (NFS) is a protocol that allows the ability to transfer files between different computers and is available on many systems, including MS Windows and Linux.
(NFS or mountd).
We can check the files being shared with `showmount` command.

#### Port Forwarding with SSH
```
ssh  user@192.168.1.1 -L 2049:127.0.0.1:2049
```
Nmap Scan on SSH portforward localhost 127.0.0.1
```
> nmap -p 2049 -sC -sV 127.0.0.1
PORT     STATE SERVICE VERSION
2049/tcp open  nfs     3-4 (RPC #100003)

Make a temp folder in current directory
> sudo mount -t nfs 127.0.0.1: tmp
> cd tmp
```

