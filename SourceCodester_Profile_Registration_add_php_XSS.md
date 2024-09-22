# XSS vulnerability from Sourcecodester Profile Registration without Reload/Refresh 1.0 (add.php)
## CVE-2024-9092

> A vulnerability was found in SourceCodester Profile Registration without Reload Refresh 1.0. It has been rated as problematic. Affected by this issue is some unknown processing of the file add.php of the component Registration Form. The manipulation of the argument full_name with an unknown input leads to a cross site scripting vulnerability. Using CWE to declare the problem leads to CWE-79. The product does not neutralize or incorrectly neutralizes user-controllable input before it is placed in output that is used as a web page that is served to other users. Impacted is integrity.

**Affected Project**: Profile Registration without Reload/Refresh

**Official Website**: https://www.sourcecodester.com/php/17587/profile-registration-without-reloadrefresh-using-ajax-php-and-mysql-source-code.html

**Version**: 1.0

**Related Code file**: add.php

**Injection parameter**: full_name

## Vulnerability Description

The **full_name** parameter is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage:
`<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration
Below is how Profile Registration without Reload/Refresh System looks like:

![index](https://github.com/user-attachments/assets/1b5e766b-6e1d-4d14-9ba3-043e09bc924f)

Below is the admin page:

![admin-php](https://github.com/user-attachments/assets/059c0702-3f4d-4791-994c-0df4631302b9)

We can register as such:

![Screenshot from 2024-09-22 15-03-46](https://github.com/user-attachments/assets/2692aaee-0dd9-4f23-9df9-0cd34ff6d961)

Intercept the registration (add.php) traffic using Burp Suite and inject the following payload:

![Screenshot from 2024-09-22 15-06-49](https://github.com/user-attachments/assets/fb7c6ef1-c680-4e54-95ff-3148bb23e416)

Payload used above is HTML encoded and decodes as `<IMG """><SCRIPT>alert("XSS")</SCRIPT>">`

Upon sending the modifying traffic containing XSS payload, we can verify the vulnerability from admin.php page:

![Screenshot from 2024-09-22 15-07-47](https://github.com/user-attachments/assets/b88b0537-b33e-4c4f-8e04-260a450ed956)
