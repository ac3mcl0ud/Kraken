#### Sending Email with Netcat

```
$ nc localhost 25
HELO localhost 
MAIL FROM: user@localhost.com
250 2.1.5 Ok
RCPT TO: root@localhost.com
250 2.1.5 Ok
DATA

Subject: Test Message
Hello Root!

.
QUIT
```
