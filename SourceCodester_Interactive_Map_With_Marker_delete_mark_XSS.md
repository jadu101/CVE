
# XSS vulnerability from Sourcecodester Interactive Map With Marker 1.0 (delete-mark.php)

**Affected Project**: Interactive Map with Marker 1.0

**Official Website**: https://www.sourcecodester.com/php/17354/interactive-map-markers-using-php-and-mysql-source-code.html#google_vignette

**Version**: 1.0

**Related Code file**: delete-mark.php

**Injection parameter**: mark

## Vulnerability Description

The **mark** parameter is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage:
`<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the **mark** input, this script could be executed in the user's browser, leading to an XSS attack.


## Demonstration

Below is how Interactive Map with Marker looks like:

![Screenshot from 2024-08-25 10-19-01](https://github.com/user-attachments/assets/3065f814-0e76-48fe-b8dc-5c581d4d8cc6)

We can delete mark as such:

![Screenshot from 2024-08-25 10-20-13](https://github.com/user-attachments/assets/7aecc58e-caf1-4b32-a0d0-c7667bfc739a)

Intercept the delete(delete-mark.php) traffic using Burp Suite and inject the following payload:

`%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`

![Screenshot from 2024-08-25 10-21-30](https://github.com/user-attachments/assets/b7368e79-91e2-40bc-b82d-a1e99e357779)

Payload used above is HTML encoded and decodes as `<IMG """><SCRIPT>alert("XSS")</SCRIPT>">`

Upon sending the modifying traffic containing XSS payload, we can verify the vulnerability:

![Screenshot from 2024-08-25 10-21-37](https://github.com/user-attachments/assets/54a1ad5b-4179-4d1e-801e-1e19a06f7d67)

