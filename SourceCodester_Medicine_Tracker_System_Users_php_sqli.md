# SQL Injection vulnerability was discovered from Sourcecodester Medicine Tracker System (Users.php)
Affected Project: Sourcecodester Medicine Tracker System 1.

Official Website: [https://www.sourcecodester.com/php/15689/food-ordering-management-system-php-and-mysql-free-source-code.html](https://www.sourcecodester.com/php/16308/medicine-tracker-system-php-oop-and-mysql-db-source-code-free-download.html)

Version: 1.0

Related Code file: /php-mts/classes/Users.php

Injection parameter: POST parameter 'MULTIPART username' is vulnerable

## Demonstration

Below is app/register.php:

![image](https://github.com/jadu101/CVE/assets/76433661/a38f7b10-60e7-467d-bc9c-c5928b2f809b)

We will intercept the create account traffic using Burp Suite:

![image](https://github.com/jadu101/CVE/assets/76433661/afe31158-de82-4abb-b83a-a8b82a17bbbb)

After saving the intercepted request as register.txt, we will run sqlmap against it:

![image](https://github.com/jadu101/CVE/assets/76433661/80458896-e659-4205-87b8-9d5e656ccdc4)
