# SQL Injection vulnerability from phpgurukul Boat Booking System 1.0 (/admin/index.php)
## CVE-2024-10156

> A vulnerability was found in PHPGurukul Boat Booking System 1.0. It has been declared as critical. This vulnerability affects an unknown code of the file /admin/index.php of the component Sign In Page. The manipulation of the argument username with an unknown input leads to a sql injection vulnerability. The CWE definition for the vulnerability is CWE-89. The product constructs all or part of an SQL command using externally-influenced input from an upstream component, but it does not neutralize or incorrectly neutralizes special elements that could modify the intended SQL command when it is sent to a downstream component. As an impact it is known to affect confidentiality, integrity, and availability.



**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: /admin/index.php

**Injection parameter**: username

## Vulnerability Description

When attempting to login as the admin, **username** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Users can try to access admin dashboard:

![Screenshot from 2024-10-17 11-27-09](https://github.com/user-attachments/assets/524ed1e8-5aea-4d41-b66b-175a7b5558c6)

Intercept the login traffic using Burp Suite:

![Screenshot from 2024-10-17 11-27-17](https://github.com/user-attachments/assets/f1762254-6521-4182-9c81-6d86c1dfff3f)

Now copy-paste the traffic and save it in to `admin-login.req` and run `sqlmap` against it: `sqlmap -r admin-login.req --batch`

`sqlmap` automatically exploit the vulnerability:

![Screenshot from 2024-10-17 11-28-26](https://github.com/user-attachments/assets/cf768407-d76a-4444-866e-9adac4172465)
