# SQL Injection vulnerability from phpgurukul Boat Booking System 1.0 (/admin/bwdates-report-details.php)

**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: /admin/bwdates-report-details.php

**Injection parameter**: fdate

## Vulnerability Description

When interacting with B/w Dates Report, **fdate** parameter is vulnerable to SQL injection vulnerability.

## Demonstration

User can interact with B/w Dates Report as such:

![Screenshot from 2024-10-17 13-23-41](https://github.com/user-attachments/assets/7ac83c70-6733-4e80-8a31-147f20bb234a)

Intercept the traffic using Burp Suite:

![Screenshot from 2024-10-17 13-23-50](https://github.com/user-attachments/assets/711da061-b7cd-41bd-b052-4fbf6d3f71d5)

Now copy-paste the traffic and save it in to `report.req` and run `sqlmap` against it: `sqlmap -r report.req --batch`

`sqlmap` automatically exploit the vulnerability:

![Screenshot from 2024-10-17 13-24-00](https://github.com/user-attachments/assets/da822ab5-2875-487e-aa8b-c67c63239bb1)
