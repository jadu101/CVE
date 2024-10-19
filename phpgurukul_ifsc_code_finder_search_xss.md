# XSS vulnerability from phpgurukul IFSC Code Finder 1.0 (search.php)

**Affected Project**: IFSC Code Finder 1.0

**Official Website**: https://phpgurukul.com/ifsc-code-finder-project-using-php/

**Version**: 1.0

**Related Code file**: search.php

## Vulnerability Description

`search.php` is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22XSS%22)%3c%2fSCRIPT%3e%22%3e`. 
This string is encoded and when decoded, it attempts to inject a script into the webpage: `<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`.

Application does not properly sanitize or validate the `searchifsccode` input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration

Below is how `search.php` looks like:

![Screenshot from 2024-10-19 13-47-56](https://github.com/user-attachments/assets/5b0858e3-dfd3-41c6-b0d3-ac171dc64141)

Let's search with the payload: `<IMG """"><SCRIPT>alert("XSS")</SCRIPT>">`

![Screenshot from 2024-10-19 13-48-03](https://github.com/user-attachments/assets/32f33859-0f46-4d23-9ead-b9af8bb5e8a2)

XSS is triggered:

![image](https://github.com/user-attachments/assets/8bb85399-bab1-40fb-a4c5-4c613b3d2326)
