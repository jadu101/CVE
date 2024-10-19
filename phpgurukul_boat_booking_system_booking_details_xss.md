# XSS vulnerability from phpgurukul Boat Booking System 1.0 (booking-details.php)
## CVE-2024-10191

> A vulnerability, which was classified as problematic, was found in PHPGurukul Boat Booking System 1.0. This affects some unknown processing of the file /admin/book-details.php of the component Booking Details Page. The manipulation of the argument Official Remark with an unknown input leads to a cross site scripting vulnerability. CWE is classifying the issue as CWE-79. The product does not neutralize or incorrectly neutralizes user-controllable input before it is placed in output that is used as a web page that is served to other users. This is going to have an impact on integrity.



**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: book-details.php

## Vulnerability Description

`booking-details.php` is vulnerable to the tested XSS payload: `%3cIMG%20%22%22%22%3e%3cSCRIPT%3ealert(%22Test%22)%3c%2fSCRIPT%3e%22%3e`. This string is encoded and when decoded, it attempts to inject a script into the webpage: `<IMG """"><SCRIPT>alert("Test")</SCRIPT>">`

Application does not properly sanitize or validate the `officialremark` input, this script could be executed in the user's browser, leading to an XSS attack.

## Demonstration

Below is how `book-details.php` looks like:

![Screenshot from 2024-10-17 14-38-13](https://github.com/user-attachments/assets/9ca8e69f-332a-4e8c-8057-c5208ba130dc)

Upon submitting, boooking details got updated successfully:

![Screenshot from 2024-10-17 14-39-11](https://github.com/user-attachments/assets/fad0790a-70a3-42cb-ae4d-8bea7965dedd)

Go visit the booking details of the modified input and we will get the XSS triggered:

![Screenshot from 2024-10-17 14-39-34](https://github.com/user-attachments/assets/84d1011a-b032-4f48-a20c-0f2e6fc6cf07)

