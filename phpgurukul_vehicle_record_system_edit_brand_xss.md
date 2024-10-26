# XSS vulnerability from phpgurukul Vehicle Record System 1.0 (edit-brand.php)
## CVE-2024-10414

> A vulnerability has been found in PHPGurukul Vehicle Record System 1.0 and classified as problematic. This vulnerability affects unknown code of the file /admin/edit-brand.php. The manipulation of the argument Brand Name leads to cross site scripting. This vulnerability was named CVE-2024-10414. The attack can be initiated remotely. Furthermore, there is an exploit available. The initial researcher advisory mentions the parameter "phone_number" to be affected. But this might be a mistake because the textbox field label is "Brand Name".



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

After submitting the change, XSS is triggered:

![Screenshot from 2024-10-25 23-13-11](https://github.com/user-attachments/assets/01a13211-4b5c-4cd3-ab02-fbbbe2f2bf56)
