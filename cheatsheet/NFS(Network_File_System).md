

#### Network File System (NFS) is a protocol that allows the ability to transfer files between different computers and is available on many systems, including MS Windows and Linux.
(NFS or mountd).
We can check the files being shared with `showmount` command.

```
Port: 2049/tcp open  mountd   1-3 (RPC #100005)
showmount -e 192.168.1.1
mkdir tmp1
sudo mount 192.168.1.1:/confidential tmp1
```

