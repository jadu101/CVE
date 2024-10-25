# XSS vulnerability from phpgurukul Vehicle Record System 1.0 (edit-brand.php)


**Affected Project**: Vehicle Record System 1.0

**Official Website**: https://phpgurukul.com/vehicle-record-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: edit-brand.php

## Vulnerability Description

`/admin/edit-brand.php` is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage: `<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the phone_number input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration

Below is how `edit-brand.php` looks like:

![Screenshot from 2024-10-25 23-13-31](https://github.com/user-attachments/assets/b71c7dad-ef18-4e21-a740-f25bc1c4a7cc)


Let's fill in some XSS payloads to it:

![Screenshot from 2024-10-25 23-13-41](https://github.com/user-attachments/assets/08f52c5a-742b-40a9-991c-b5496518c4aa)

Now, sign in as the admin:

![Screenshot from 2024-10-17 11-16-19](https://github.com/user-attachments/assets/3966cfcb-0946-4ad7-b761-d8506a84c4f0)

Going to `all-booking.php`, XSS payload is triggered:

![Screenshot from 2024-10-17 11-16-34](https://github.com/user-attachments/assets/6e63367c-3770-4a1f-9092-539b8f939066)

Using this, attacker can potentially steal admin's session Cookie. 
