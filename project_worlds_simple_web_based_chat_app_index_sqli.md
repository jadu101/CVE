# SQL Injection vulnerability from Project Worlds Simple Web Based Chat Application 1.0 (/index.php)

**Affected Project**: Simple Web Based Chat Application 1.0

**Official Website**: https://projectworlds.in/simple-web-based-chat-application-using-php-mysql-javascript-ajax/

**Version**: 1.0

**Related Code file**: index.php

**Injection parameter**: username

## Vulnerability Description

When sendming message, **username** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

User can send message as such:

![Screenshot from 2024-10-27 02-08-35](https://github.com/user-attachments/assets/ff2dee0c-9e44-4efb-845b-e52541ce93c7)

Intercept the traffic using Burp Suite:

![Screenshot from 2024-10-27 02-11-55](https://github.com/user-attachments/assets/f655cce8-3080-435e-a53e-2252b8883549)

Now copy-paste the traffic and save it in to `send.req` and run `sqlmap` against it: `sqlmap -r send.req --batch --level 5 --risk 3 --dbms mysql`

`sqlmap` automatically exploits the vulnerability:

![image](https://github.com/user-attachments/assets/b9c314b1-4c60-4f77-ba03-20a6fcf2ec74)
