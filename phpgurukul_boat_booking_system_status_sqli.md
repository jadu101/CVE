# SQL Injection vulnerability from phpgurukul Boat Booking System 1.0 (status.php)
## CVE-2024-10154

**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: status.php

**Injection parameter**: emailid

## Vulnerability Description

When checking the boat booking status, **emailid** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

Users can check their boat booking status as such:

![Screenshot from 2024-10-17 10-59-05](https://github.com/user-attachments/assets/482c6b2b-7438-4bcd-8df9-133ebbb235f4)

Intercept the status check traffic using Burp Suite:

![Screenshot from 2024-10-17 11-04-51](https://github.com/user-attachments/assets/260dcd62-7783-41df-8bb1-80f58b0345b4)

Now copy-paste the traffic and save it in to `status.req` and run `sqlmap` against it: `sqlmap -r status.req --batch`

`sqlmap` automatically exploit the vulnerability:

![Screenshot from 2024-10-17 11-05-37](https://github.com/user-attachments/assets/4d154556-7670-44e1-bf36-0cca8beaf912)
