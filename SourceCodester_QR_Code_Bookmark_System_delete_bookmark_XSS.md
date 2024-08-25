
# XSS vulnerability from Sourcecodester QR Code Bookmark System 1.0 (delete-bookmark.php)

**Affected Project**: QR Code Bookmark System 1.0

**Official Website**: https://www.sourcecodester.com/php/17286/qr-code-bookmark-system-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: delete-bookmark.php

**Injection parameter**: bookmark

## Vulnerability Description

The **bookmark** parameter is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage:
`<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration
Below is how QR Code Bookmark System looks like:

![Screenshot from 2024-08-25 10-58-50](https://github.com/user-attachments/assets/ea1d467c-872b-434d-9039-2d4638a861d5)

We can delete bookmark as such:

![Screenshot from 2024-08-25 11-10-55](https://github.com/user-attachments/assets/df7ca1dc-3b79-4bbe-b837-e630a11eea05)

Intercept the delete(delete-bookmark.php) traffic using Burp Suite and inject the following payload:

![Screenshot from 2024-08-25 11-11-20](https://github.com/user-attachments/assets/59051aec-84f4-4a6e-ad59-5ef1fd253fcf)

Payload used above is HTML encoded and decodes as `<IMG """><SCRIPT>alert("XSS")</SCRIPT>">`

Upon sending the modifying traffic containing XSS payload, we can verify the vulnerability:

![Screenshot from 2024-08-25 11-00-50](https://github.com/user-attachments/assets/28168943-a37b-473f-bdc5-26c78ede3034)
