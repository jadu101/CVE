# SQL Injection vulnerability from phpgurukul Student Project Allocation System 1.0 (add_project.php)

**Affected Project**: Student Project Allocation System 1.0

**Official Website**: https://projectworlds.in/student-project-allocation-system-using-php-with-source-code/

**Version**: 1.0

**Related Code file**: add_project.php

**Injection parameter**: project_id

## Vulnerability Description

When adding project, **project_id** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Below is how `project_selection.php` looks like:

![Screenshot from 2024-10-26 14-19-41](https://github.com/user-attachments/assets/50b96b6b-0a66-4f53-9449-3d8d88b82786)

Click on `Add` and intercept the traffic using Burp Suite:

![Screenshot from 2024-10-26 14-28-13](https://github.com/user-attachments/assets/ca59faf5-3295-4829-8a47-2f0aaf6955b6)

Now copy-paste the traffic and save it in to `add_project.req` and run `sqlmap` against it: `sqlmap -r add_project.req --batch --dbms mysql --level 5 --risk 3 -p project_id`

`sqlmap` automatically exploits the vulnerability:

![Screenshot from 2024-10-26 14-29-00](https://github.com/user-attachments/assets/0404a597-ca93-4fd8-95c8-28d204344ba7)
