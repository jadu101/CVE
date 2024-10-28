# SQL Injection vulnerability from Project Worlds Online Time Table Generator 1.0 (/admindashboard.php)
## CVE-2024-10446
> A vulnerability classified as critical was found in Project Worlds Online Time Table Generator 1.0. Affected by this vulnerability is an unknown functionality of the file /timetable/admin/admindashboard.php?info=add_course. The manipulation of the argument c leads to sql injection. This vulnerability is known as CVE-2024-10446. The attack can be launched remotely. Furthermore, there is an exploit available.




**Affected Project**: Online Time Table Generator 1.0

**Official Website**: https://projectworlds.in/online-time-table-generator-php-mysql/

**Version**: 1.0

**Related Code file**: admindashboard.php

**Injection parameter**: `MULTIPART c`

## Vulnerability Description

When adding a new department as the admin, **MULTIPART C** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Admin can add department as such:

![Screenshot from 2024-10-27 15-34-23](https://github.com/user-attachments/assets/e0ff9948-8ce0-4307-9c5b-b7835c86cb8f)

Intercept the traffic using Burp Suite:

![Screenshot from 2024-10-27 15-34-51](https://github.com/user-attachments/assets/85c33a37-4904-4d7b-b063-ae4bf126b10a)

Now copy-paste the traffic and save it in to `add_dept.req` and run `sqlmap` against it: `sqlmap -r add_dept.req --batch --level 5 --risk 3 --dbms mysql`

`sqlmap` automatically exploits the vulnerability:

![Screenshot from 2024-10-27 15-35-31](https://github.com/user-attachments/assets/cb494fae-da21-4fd8-91bc-7205cd5c699c)
