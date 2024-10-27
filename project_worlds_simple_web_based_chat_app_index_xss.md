# XSS vulnerability from Project Worlds Simple Web Based Chat Application 1.0 (/index.php)
## CVE-2024-10433

> A vulnerability was found in Project Worlds Simple Web-Based Chat Application 1.0. It has been classified as problematic. This affects an unknown part of the file /index.php. The manipulation of the argument Name/Comment leads to cross site scripting. This vulnerability is uniquely identified as CVE-2024-10433. It is possible to initiate the attack remotely. Furthermore, there is an exploit available. The initial researcher advisory mentions different parameters to be affected which do not correlate with the screenshots of a successful attack.


**Affected Project**: Simple Web Based Chat Application 1.0

**Official Website**: https://projectworlds.in/simple-web-based-chat-application-using-php-mysql-javascript-ajax/

**Version**: 1.0

**Related Code file**: index.php

**Injection parameter**: username

## Vulnerability Description

`index.php` is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage: `<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

Application does not properly sanitize or validate the phone_number input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration

Below is how `index.php` looks like:

![Screenshot from 2024-10-27 02-09-52](https://github.com/user-attachments/assets/c3cae90a-8f8a-4b40-a6e9-67769255eef2)

Let's fill in some XSS payloads to it:

![Screenshot from 2024-10-27 02-20-16](https://github.com/user-attachments/assets/abe61b99-69ad-4614-a1d4-b9d56a46b063)

After submitting the change, XSS is triggered:

![Screenshot from 2024-10-27 02-19-28](https://github.com/user-attachments/assets/6059ff6c-cb48-4949-8d72-196c12cd8f65)
