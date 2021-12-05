### How does an LFI Attack Work

A Local File Inclusion can occur when an application includes a file as user input without properly validating it. This flaw enables an attacker to include malicious files by manipulating the input.

The following vulnerable PHP code could lead to LFI:

> https://website-example.com/?page=filename.php

> https://website-example.com/?page=../../../../etc/test.txt

> http://www.example_target_website.com/download.php?file=document.html
