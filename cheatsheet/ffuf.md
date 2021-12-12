#### FFUF
* Directory Fuzzing with ffuf.
```
ffuf -u http://192.168.1.1/FUZZ -t 100 -sf -e php,txt,html,js -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
```
* WFUZZ
```
wfuzz -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://192.168.1.1/ --hc 301 -v -c -H "Host:FUZZ.192.168.1.1.com"
