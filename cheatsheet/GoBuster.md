#### Gobuster Scan
  ```
  sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://TARGET_IP/
  ```
  ```
  sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://TARGET_IP/ -x php,py,js,css,html,txt
  ```
  ```
  sudo gobuster dir -w /usr/share/wordlists/dirb/common.txt -u http://TARGET_IP/ -x php,py,js,css,html,txt
  ```
