
# XSS vulnerability from Sourcecodester QR Code Attendance System 1.0 (delete-student.php)

**Affected Project**: QR Code Attendance System 1.0

**Official Website**: https://www.sourcecodester.com/php/17242/qr-code-attendance-system-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: delete-student.php

**Injection parameter**: student

## Vulnerability Description

The **student** parameter is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage:
`<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration
Below is how QR Code Attendance System looks like:

![Screenshot from 2024-08-25 23-41-57](https://github.com/user-attachments/assets/587643a5-a670-405f-80c5-a91ee76c1f27)

We can delete student as such:

![Screenshot from 2024-08-25 23-47-11](https://github.com/user-attachments/assets/eb41da60-ff06-4802-a657-5f915018dcf8)

Intercept the delete(delete-student.php) traffic using Burp Suite and inject the following payload:

![Screenshot from 2024-08-25 23-47-39](https://github.com/user-attachments/assets/113398ad-a44d-4955-82c4-36a3c58afc58)

Payload used above is HTML encoded and decodes as `<IMG """><SCRIPT>alert("XSS")</SCRIPT>">`

Upon sending the modifying traffic containing XSS payload, we can verify the vulnerability:

![Screenshot from 2024-08-25 23-47-45](https://github.com/user-attachments/assets/f4a983fa-a304-48cc-8dbf-cd7c8b8ec95a)
