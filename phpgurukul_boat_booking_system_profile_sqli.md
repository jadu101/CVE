# SQL Injection vulnerability from phpgurukul Boat Booking System 1.0 (/admin/profile.php)
## CVE-2024-10159


**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: /admin/profile.php

**Injection parameter**: mobilenumber

## Vulnerability Description

When editing profile, **mobilenumber** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Below is how `profile.php` looks like:

![Screenshot from 2024-10-17 13-13-38](https://github.com/user-attachments/assets/544d8c48-f07a-431b-ae51-29889fb42100)

Intercept the profile update traffic using Burp Suite:

![Screenshot from 2024-10-17 13-14-29](https://github.com/user-attachments/assets/257c5707-ef84-47a7-8689-6afaee0bfa6a)

Now copy-paste the traffic and save it in to `profile-edit.req` and run `sqlmap` against it: `sqlmap -r profile-edit.req --batch`

`sqlmap` automatically exploit the vulnerability:

![Screenshot from 2024-10-17 13-14-56](https://github.com/user-attachments/assets/e170d241-1ab6-4247-ae48-2b5b57eb0000)
