# SQL Injection vulnerability from phpgurukul Boat Booking System 1.0 (book-boat.php)
**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: book-boat.php

**Injection parameter**: nopeople

## Vulnerability Description

When booking a boat, **nopeople** parameter is vulnerable to SQL injection vulnerability.

## Demonstration
Below is how boat booking system looks like:

![Screenshot from 2024-10-17 10-41-18](https://github.com/user-attachments/assets/78ed07f8-0f9a-49da-b904-7ae0775da89d)


Let's fill in some random information to it:

![Screenshot from 2024-10-17 10-41-43](https://github.com/user-attachments/assets/4387680e-5df0-46da-bda4-ea8ca3e2efbb)

Intercept the boat booking traffic using Burp Suite:

![Screenshot from 2024-10-17 10-42-55](https://github.com/user-attachments/assets/939a59c2-d7aa-4725-85f0-8b59dd4b0f73)

Now copy-paste the traffic and save it in to `book-boat.req` and run `sqlmap` against it: `sqlmap -r book-boat.req --batch`

`sqlmap` automatically exploit the vulnerability:

![Screenshot from 2024-10-17 10-43-20](https://github.com/user-attachments/assets/ce58be7b-10d1-42eb-93d0-270aa6bab7ba)
