#### FFUF
* Directory Fuzzing with ffuf.
```
ffuf -u http://192.168.1.1/FUZZ -t 100 -sf -e php,txt,html,js -w /usr/share/Seclists/Discovery/Web-Content/raft-medium-directories.txt
```
