#### Sending Email with Netcat

```
$ nc localhost 25
HELO localhost 
MAIL FROM: user@localhost.com
RCPT TO: root@localhost.com
DATA

Subject: Test Message
Hello Root!

.
QUIT
```
