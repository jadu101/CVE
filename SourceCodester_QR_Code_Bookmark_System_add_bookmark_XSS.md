
# XSS vulnerability from Sourcecodester QR Code Bookmark System 1.0 (add-bookmark.php)

**Affected Project**: QR Code Bookmark System 1.0

**Official Website**: https://www.sourcecodester.com/php/17286/qr-code-bookmark-system-using-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: add-bookmark.php

**Injection parameter**: name, url

## Vulnerability Description

The **name**, **url** parameters are vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage:
`<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration
Below is how QR Code Bookmark System looks like:

![Screenshot from 2024-08-25 10-58-50](https://github.com/user-attachments/assets/ea1d467c-872b-434d-9039-2d4638a861d5)

We can add bookmark as such:

![Screenshot from 2024-08-25 10-59-29](https://github.com/user-attachments/assets/4ce89c6e-c5de-43e3-9538-a717651ddcca)

Intercept the add(add-bookmark.php) traffic using Burp Suite and inject the following payload:

`%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`

![Screenshot from 2024-08-25 11-00-27](https://github.com/user-attachments/assets/66623a94-6c52-4066-97d8-0ade7d549755)

Payload used above is HTML encoded and decodes as `<IMG """><SCRIPT>alert("XSS")</SCRIPT>">`

Upon sending the modifying traffic containing XSS payload, we can verify the vulnerability:

![Screenshot from 2024-08-25 11-00-50](https://github.com/user-attachments/assets/28168943-a37b-473f-bdc5-26c78ede3034)

