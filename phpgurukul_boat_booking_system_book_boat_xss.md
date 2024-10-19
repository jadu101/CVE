# XSS vulnerability from phpgurukul Boat Booking System 1.0 (book-boat.php)
## CVE-2024-10155

> A vulnerability was found in PHPGurukul Boat Booking System 1.0. It has been classified as problematic. This affects an unknown part of the file book-boat.php?bid=1 of the component Book a Boat Page. The manipulation of the argument phone_number with an unknown input leads to a cross site scripting vulnerability. CWE is classifying the issue as CWE-79. The product does not neutralize or incorrectly neutralizes user-controllable input before it is placed in output that is used as a web page that is served to other users. This is going to have an impact on integrity.



**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: book-boat.php, all-booking.php

## Vulnerability Description

`book-boat.php` and `/admin/all-booking.php` is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage: `<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the phone_number input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration

Below is how boat booking system looks like:

![Screenshot from 2024-10-17 10-41-18](https://github.com/user-attachments/assets/78ed07f8-0f9a-49da-b904-7ae0775da89d)


Let's fill in some XSS payloads to it:

![Screenshot from 2024-10-17 11-11-37](https://github.com/user-attachments/assets/c8a96fee-edd8-4395-b9da-d125606f0626)

Now, sign in as the admin:

![Screenshot from 2024-10-17 11-16-19](https://github.com/user-attachments/assets/3966cfcb-0946-4ad7-b761-d8506a84c4f0)

Going to `all-booking.php`, XSS payload is triggered:

![Screenshot from 2024-10-17 11-16-34](https://github.com/user-attachments/assets/6e63367c-3770-4a1f-9092-539b8f939066)

Using this, attacker can potentially steal admin's session Cookie. 
