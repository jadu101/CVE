![image](https://github.com/user-attachments/assets/a7e737e5-bee5-438e-a359-d029b57cbf2b)# Arbitrary File upload vulnerability from phpgurukul Boat Booking System 1.0 (change-image.php)

**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: change-image.php

## Vulnerability Description

User can update boat image through `change-image.php`. 

Web application doesn't sanitize or filters the image being uploaded, making it vulnerable to arbitrary file upload vulnerability, that can also lead to Remote Code Execution. 

## Demonstration

Below is how `change-image.php` looks like:

![Screenshot from 2024-10-17 13-43-03](https://github.com/user-attachments/assets/74d34d40-bb36-47a8-9ec1-744902680a31)

Let's upload random image and intercept the upload traffic using Burp Suite:

![Screenshot from 2024-10-17 13-43-26](https://github.com/user-attachments/assets/9dc020a7-2b9f-4b4e-b7ae-000a148ad3ff)

On Burp Suite intruder, we can try sending with various file extensions and content-type and everything will get accepted:

![Screenshot from 2024-10-17 13-43-55](https://github.com/user-attachments/assets/64474e5e-c37c-4f7f-b35f-10381ee65a26)

Going to the main website, we can see that the our file was uploaded successfully:

![image](https://github.com/user-attachments/assets/ea9c581d-3202-4451-896a-12c8a7c24a0c)

