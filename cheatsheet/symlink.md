#### Create a shortcut to run an application from anywhere.

```
#!/usr/bin/env sh

set -e

cd /home/kali/tools
exec ./kerbrute_linux_amd64 "$@"
```
