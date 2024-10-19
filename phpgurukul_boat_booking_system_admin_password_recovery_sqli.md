# SQL Injection vulnerability from phpgurukul Boat Booking System 1.0 (/admin/password-recovery.php)
## CVE-2024-10157

> A vulnerability was found in PHPGurukul Boat Booking System 1.0. It has been rated as critical. This issue affects an unknown code block of the file /admin/password-recovery.php of the component Reset Your Password Page. The manipulation of the argument username with an unknown input leads to a sql injection vulnerability. Using CWE to declare the problem leads to CWE-89. The product constructs all or part of an SQL command using externally-influenced input from an upstream component, but it does not neutralize or incorrectly neutralizes special elements that could modify the intended SQL command when it is sent to a downstream component. Impacted is confidentiality, integrity, and availability.


**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: /admin/password-recovery.php

**Injection parameter**: username

## Vulnerability Description

When attempting to reset the password, **username** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Users can try to reset the password:

![Screenshot from 2024-10-17 11-33-12](https://github.com/user-attachments/assets/3fd24446-47ed-4abc-97f6-7c4590e58e05)

Intercept the traffic using Burp Suite:

![Screenshot from 2024-10-17 11-33-27](https://github.com/user-attachments/assets/a2b27a63-11b7-4825-acb2-f3fcbea9e0fa)

Now copy-paste the traffic and save it in to `reset-pwd.req` and run `sqlmap` against it: `sqlmap -r reset-pwd.req --batch`

`sqlmap` automatically exploit the vulnerability:

![Screenshot from 2024-10-17 11-35-59](https://github.com/user-attachments/assets/eaee8439-a4b1-4473-a645-1c271a845247)
