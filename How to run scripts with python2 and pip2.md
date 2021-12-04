## How to run scripts with python2 and pip2?

As we all know that we backwards compatibility issues when trying to run python2 scripts in Kali Linux 2020 and above. 

The issue is with python2 and pip2. 

This is will also help you installing the right version of impacket for python2.

We will try to run the Andyacer's MS08_067 Python Exploit Script. 

This script is python2 and requires python2 pip2 impacket and pycrypto.

Link: https://github.com/andyacer/ms08_067 

### NOTE: Before you do any of the steps below, if you’re running your distro in VMware or VirtualBox. You might want to take a backup.
In this tutorial we cover how to run python2 scripts in newer version of Kali Linux.

## 1.	First check the versions of python2 and python3 installed in your distro.

`$ python2 –version`
 
Python 2.7.18

`$ python3 –version`
 
Python 3.9.2

## 2.	Download the installer script for pip2 and pip3.

### NOTE: Install the PIP version in the following order. Starting with PIP2 first followed PIP3.

You also can create a folder for pip installer script:

`$ mkdir <folder_name> in your home directory.`

And then CD into it.

### PIP2:

Link: https://bootstrap.pypa.io/pip/2.7/get-pip.py

`$ wget https://bootstrap.pypa.io/pip/2.7/get-pip.py`

### PIP3:

Link: https://bootstrap.pypa.io/get-pip.py

`$ wget https://bootstrap.pypa.io/get-pip.py`

Now if you LS you will should have two versions of get-pip.py

Possible output: get-pip.py(pip for python3)  get-pip.py.1(pip for python2)

## 3.	Let’s install the pip.

First, we need to install PIP2

`$ sudo python2 get-pip.py.1`
 
You will get DEPRECATION WARNING for python2, but that’s ok

The output should look like this: 

Installing collected packages: pip, wheel

> Successfully installed pip-20.3.4 wheel-0.37.0

Next, we will install PIP3.

`$ sudo python3 get-pip.py`
The output should look like this:

> Installing collected packages: wheel, pip

> Successfully installed pip-21.2.4 wheel-0.37.0

## 4.	 Now we can check the PIP versions

`$ pip2 –version`

> pip 20.3.4 from /usr/local/lib/python2.7/dist-packages/pip (python 2.7)

`$ pip3 –version`

>pip 21.2.4 from /usr/local/lib/python3.9/dist-packages/pip (python 3.9)

Default PIP version:
`$ pip –version`

> pip 21.2.4 from /usr/local/lib/python3.9/dist-packages/pip (python 3.9)

## 5.	Let’s install a python2 script [exploit] by Andyacer to verify our python2 pip installation is working.

Link: https://github.com/andyacer/ms08_067/

`$ git clone https://github.com/andyacer/ms08_067/`

We will also need to install impacket and pycrypto for pip2 version to make the script run.

`$ git clone --branch impacket_0_9_17 --single-branch https://github.com/CoreSecurity/impacket/`
 
`$ cd impacket`
 
`$ pip2 install .`

Possibly you will get an error for compiling pycrypto for compiling.

Something like this: Failed to build pycrypto

To fix this we need to install: (necessary)

`$ sudo apt-get install build-essential libssl-dev libffi-dev `
 
`$ sudo apt-get install python2.7-dev`
 
`$ pip2 install --upgrade setuptools`

Now you can run:

`$ pip2 install .`

If everything goes well.

You should get and output something like this.

> Successfully installed Jinja2-2.11.3 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.2 cryptography-3.3.2 dnspython-1.16.0 enum34-1.1.10 flask-1.1.4 future-0.18.2 impacket-0.9.17 ipaddress-1.0.23 itsdangerous-1.1.0 ldap3-2.9.1 ldapdomaindump-0.9.3 pyOpenSSL-20.0.1 pycrypto-2.6.1 six-1.16.0

You can also verify the installation with.

`$ pip2 install pycrypto`
> 
Your output should look like this.

> DEPRECATION: Python 2.7 reached the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 is no longer maintained. pip 21.0 will drop support for Python 2.7 in January 2021. More details about Python 2 support in pip can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support pip 21.0 will remove support for this functionality.
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: pycrypto in /home/<YOUR_NAME>/.local/lib/python2.7/site-packages (2.6.1)

## 6.	Finally, let’s CD into the script directory 

`$ cd ms08_067`

And run with python2

`$ python ms08_067_2018.py

MS08-067 Exploit

This is a modified verion of Debasis Mohanty's code (https://www.exploit-db.com/exploits/7132/).

The return addresses and the ROP parts are ported from metasploit module exploit/windows/smb/ms08_067_netapi

Mod in 2018 by Andy Acer:

- Added support for selecting a target port at the command line.

It seemed that only 445 was previously supported.

- Changed library calls to correctly establish a NetBIOS session for SMB transport

- Changed shellcode handling to allow for variable length shellcode. Just cut and paste

into this source file.

Usage: ms08_067_2018.py <target ip> <os #> <Port #>`
