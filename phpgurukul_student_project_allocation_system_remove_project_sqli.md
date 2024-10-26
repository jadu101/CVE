# SQL Injection vulnerability from phpgurukul Student Project Allocation System 1.0 (remove_project.php)
## CVE-2024-10424

> A vulnerability was found in Project Worlds Student Project Allocation System 1.0 and classified as critical. Affected by this issue is some unknown functionality of the file /student/project_selection/remove_project.php of the component Project Selection Page. The manipulation of the argument no leads to sql injection. This vulnerability is handled as CVE-2024-10424. The attack may be launched remotely. Furthermore, there is an exploit available.


**Affected Project**: Student Project Allocation System 1.0

**Official Website**: https://projectworlds.in/student-project-allocation-system-using-php-with-source-code/

**Version**: 1.0

**Related Code file**: remove_project.php

**Injection parameter**: no

## Vulnerability Description

When removing project, **no** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Below is how `project_selection.php` looks like:

![Screenshot from 2024-10-26 14-19-41](https://github.com/user-attachments/assets/50b96b6b-0a66-4f53-9449-3d8d88b82786)

Click on `remove` and intercept the traffic using Burp Suite:

![Screenshot from 2024-10-26 14-35-26](https://github.com/user-attachments/assets/d1d3fbcd-c56c-494f-9a1c-0f21dce1d724)

Now copy-paste the traffic and save it in to `remove_project.req` and run `sqlmap` against it: `sqlmap -r remove_project.req --batch --dbms mysql --level 5 --risk 3 -p no`

`sqlmap` automatically exploits the vulnerability:

![Screenshot from 2024-10-26 14-35-57](https://github.com/user-attachments/assets/ac70c70e-999b-4775-83e9-beadb40798d0)
