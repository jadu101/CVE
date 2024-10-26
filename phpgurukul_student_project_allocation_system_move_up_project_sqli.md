# SQL Injection vulnerability from phpgurukul Student Project Allocation System 1.0 (move_up_project.php)
## CVE-2024-10425

> A vulnerability was found in Project Worlds Student Project Allocation System 1.0. It has been classified as critical. This affects an unknown part of the file /student/project_selection/move_up_project.php of the component Project Selection Page. The manipulation of the argument up leads to sql injection. This vulnerability is uniquely identified as CVE-2024-10425. It is possible to initiate the attack remotely. Furthermore, there is an exploit available.



**Affected Project**: Student Project Allocation System 1.0

**Official Website**: https://projectworlds.in/student-project-allocation-system-using-php-with-source-code/

**Version**: 1.0

**Related Code file**: move_up_project.php

**Injection parameter**: up

## Vulnerability Description

When moving up project, **up** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Below is how `project_selection.php` looks like:

![Screenshot from 2024-10-26 14-19-41](https://github.com/user-attachments/assets/50b96b6b-0a66-4f53-9449-3d8d88b82786)

Click on `Move Up` and intercept the traffic using Burp Suite:

![Screenshot from 2024-10-26 14-44-49](https://github.com/user-attachments/assets/012c4e4b-ae38-4192-bf89-9f38d6ba1063)

Now copy-paste the traffic and save it in to `move_up_project.req` and run `sqlmap` against it: `sqlmap -r move_up_project.req --batch --dbms mysql --level 5 --risk 3 -p up`

`sqlmap` automatically exploits the vulnerability:

![Screenshot from 2024-10-26 14-45-23](https://github.com/user-attachments/assets/d6eab9eb-69d9-43ea-b781-5183fbdf2ca9)
