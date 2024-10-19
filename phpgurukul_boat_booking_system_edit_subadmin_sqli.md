# SQL Injection vulnerability from phpgurukul Boat Booking System 1.0 (/admin/edit-subadmin.php)
## CVE-2024-10162

**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: /admin/edit-subadmin.php

**Injection parameter**: mobilenumber

## Vulnerability Description

When editing subadmin profile, **mobilenumber** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Below is how `edit-subadmin.php` looks like:

![Screenshot from 2024-10-17 14-16-09](https://github.com/user-attachments/assets/1b4e640e-0334-4951-ac64-ef8dd1f8effb)

Intercept the profile update traffic using Burp Suite:

![Screenshot from 2024-10-17 14-27-13](https://github.com/user-attachments/assets/cb7ce6b5-9cf2-4869-a2ca-9caf67bba11b)

Now copy-paste the traffic and save it in to `profile-edit.req` and run `sqlmap` against it: `sqlmap -r profile-edit.req --batch`

`sqlmap` automatically exploit the vulnerability:

![Screenshot from 2024-10-17 14-27-25](https://github.com/user-attachments/assets/2e194923-badb-44c1-80d3-d5e6bf7775c3)
